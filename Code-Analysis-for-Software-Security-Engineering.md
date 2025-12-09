# Code Analysis for Software Security Engineering

[Project Board](https://github.com/orgs/CYBR-8420-Team-Open-Source-Elephant/projects/3/views/1)


----

## Part 1: Code Review

----

## Code Review Strategy 

----

## Selected CWEs

----

## Part 2: Key Findings and Contributions

----

## Automated Code Review

The full SonarQube scan results are available [here](https://sonarcloud.io/summary/overall?id=CYBR-8420-Team-Open-Source-Elephant_ERPNext-project&branch=develop). From these results, we triaged the issues and selected files that we felt were relevant to our use cases or that may have one of our selected CWEs. We focused on issues that were in the Security and Reliability categories and had one of the top two severity levels. We also looked at the Security Hotspots, which are areas in the code detected by SonarQube that may be security sensitive.

----

## Manual Code Review

We selected the following files for manual review. They all had an issue or a security hotspot detected by SonarQube and dealt with authentication, access control, logging, business logic, and external data handling.

- erpnext/accounts/doctype/coupon_code/coupon_code.js
- erpnext/setup/doctype/sales_partner/sales_partner.py
- erpnext/edi/doctype/common_code/common_code.py
- erpnext/manufacturing/doctype/sales_forecast/sales_forecast.py
- erpnext/accounts/doctype/sales_invoice/sales_invoice.py
- erpnext/setup/utils.py
- erpnext/accounts/report/share_balance/share_balance.py
- erpnext/patches/v10_0/fichier_des_ecritures_comptables_for_france.py
- erpnext/stock/doctype/item/item.js


### File: erpnext/accounts/doctype/coupon_code/coupon_code.js

#### Issue Detected by SonarQube

Make sure that using this pseudorandom number generator is safe here.

#### Analysis

```
make_coupon_code: function (frm) {
		var coupon_name = frm.doc.coupon_name;
		var coupon_code;
		if (frm.doc.coupon_type == "Gift Card") {
			coupon_code = Math.random().toString(12).substring(2, 12).toUpperCase();
		} else if (frm.doc.coupon_type == "Promotional") {
			coupon_name = coupon_name.replace(/\s/g, "");
			coupon_code = coupon_name.toUpperCase().slice(0, 8);
		}
		frm.doc.coupon_code = coupon_code;
		frm.refresh_field("coupon_code");
},
```

Gift card and promotional codes are generated in client-side JavaScript code using Math.random() (for gift cards) or a truncated coupon name (for promotions). When debugging the code in the browser's developer tools, we were able to save arbitrary coupon codes without being blocked by any backend validation. This shows that ERPNext is trusting client-controlled coupon codes for a security-sensitive feature. This could be risky if a role with coupon-creation rights is compromised or misconfigured. Additionally, using a random number generator that is not cryptographically secure could create a risk of gift card codes being guessed or brute forced.

#### Relevant CWEs

- CWE-603 (Use of Client-Side Authentication)
- CWE-272 (Least Privilege Violation)
- CWE-266 (Incorrect Privilege Assignment)
- CWE-284 (Improper Access Control)
- CWE-338 (Use of Cryptographically Weak Pseudo-Random Number Generator)

#### Mitigation

Move coupon code generation to the backend and use a cryptographically secure random number generator. Treat coupon codes supplied from the client as untrusted. Ensure that the roles that can create gift cards and coupons are restricted.

### File: erpnext/setup/doctype/sales_partner/sales_partner.py

#### Issue Detected by SonarQube

Using http protocol is insecure. Use https instead.

#### Analysis

```
def validate(self):

	if not self.route:

		self.route = "partners/" + self.scrub(self.partner_name)

	super().validate()

	if self.partner_website and not self.partner_website.startswith("http"):

		self.partner_website = "http://" + self.partner_website
```

Sales partners in ERPNext represent external entities such as distributors. The partner_website field can be saved with http:// or without any scheme. HTTPS is allowed but not enforced. There is no validation that the URL is well-formed.

#### Relevant CWEs

- CWE-200 (Information Exposure)
- CWE-319 (Cleartext Transmission of Sensitive Information)

#### Mitigation

```
from urllib.parse import urlparse
import frappe


if self.partner_website:
    url = self.partner_website.strip()

    if not url.startswith(("http://", "https://")):
        url = "https://" + url

    parsed = urlparse(url)

    if not parsed.netloc:
        frappe.throw("Invalid partner website URL")

    self.partner_website = url

```

This code shows how HTTPS could be enforced by default and adds basic validation that rejects bad URLs.

### File: erpnext/edi/doctype/common_code/common_code.py

#### Issue Detected by SonarQube

Disable access to external entities in XML parsing.

#### Analysis

The function imports a user-supplied XML genericode file using:
```
parser = etree.XMLParser(remove_blank_text=True)
tree = etree.parse(file_path, parser=parser)

```

Because this input comes from uploads, we should treat it as untrusted.

#### Relevant CWEs

- CWE-20 (Improper Input Validation)
- CWE-611 (Improper Restriction of XML External Entity Reference)

#### Mitigation

```
parser = etree.XMLParser(
    remove_blank_text=True,
    resolve_entities=False,
    load_dtd=False,
    no_network=True,
)

tree = etree.parse(file_path, parser=parser)

filters = filters or {}
filter_conditions = [
    f"Value[@ColumnRef='{column_ref}']/SimpleValue='{value}'"
    for column_ref, value in filters.items()
]

```

This code shows how the parser could be hardened to better handle untrusted input.

### File: erpnext/manufacturing/doctype/sales_forecast/sales_forecast.py

#### Issue Detected by SonarQube

Fix this code; this expression does not have a "\_\_getitem__" method.


#### Analysis

```
_sales_data = pd_sales_data.set_index("date").resample(resample_val).sum()["qty"]
```

After .sum(), the result is a Series, so ["qty"] is invalid. This would break demand generation for manufacturing.

#### Relevant CWEs

- CWE-670 (Incorrect Control Flow)

#### Mitigation

```
_sales_data = (
    pd_sales_data.set_index("date")
    .resample(resample_val)["qty"]
    .sum()
)

```

This is not directly a security issue, but it affects the reliability of planning logic in our manufacturing misuse case.

#### File: erpnext/accounts/doctype/sales_invoice/sales_invoice.py

#### Issue Detected by SonarQube

Remove this equality check between incompatible types; it will always return False.

#### Analysis

```
if invalid_modes:

	if invalid_modes == 1:
        msg = _("Please set default Cash or Bank account in Mode of Payment {}")
    else:
        msg = _("Please set default Cash or Bank account in Mode of Payments {}")
    frappe.throw(msg.format(", ".join(invalid_modes)), title=_("Missing Account"))
```

An equality check compares incompatible types in the validation logic for payment modes. This condition will never be true and appears to be legacy or “technical debt,” which can hide future bugs.

#### Relevant CWEs

- CWE-570 (Always-False Condition)
- CWE-561 (Dead Code)

#### Mitigation

```
if invalid_modes:
    if len(invalid_modes) == 1:
        msg = _("Please set default Cash or Bank account in Mode of Payment {}")
    else:
        msg = _("Please set default Cash or Bank account in Mode of Payments {}")

    frappe.throw(msg.format(", ".join(invalid_modes)), title=_("Missing Account"))
```

This ensures that the check is meaningful.

### File: erpnext/setup/utils.py

#### Issue Reported by SonarQube

"password" detected here, review this potentially hard-coded credential.

#### Analysis

```
if not frappe.db.a_row_exists("Company"):

	current_year = now_datetime().year

	setup_complete(

		{

			"currency": "USD",

			"full_name": "Test User",

			"company_name": "Wind Power LLC",

			"timezone": "America/New_York",

			"company_abbr": "WP",

			"industry": "Manufacturing",

			"country": "United States",

			"fy_start_date": f"{current_year}-01-01",

			"fy_end_date": f"{current_year}-12-31",

			"language": "english",

			"company_tagline": "Testing",

			"email": "test@erpnext.com",

			"password": "test",
            "chart_of_accounts": "Standard",

		}
    )
```

A password: "test" default appears in setup data, but login still requires email verification and it is clearly a test/demo configuration. There is low practical risk, but it reinforces the need to disable default credentials in production.

### File: erpnext/accounts/report/share_balance/share_balance.py

#### Issue Reported by SonarQube

Make sure using this hardcoded IP address "::90" is safe here.

#### Analysis

```
def get_columns(filters):

	columns = [

		_("Shareholder") + ":Link/Shareholder:150",

		_("Share Type") + "::90",
        
        _("No of Shares") + "::90",

		_("Average Rate") + ":Currency:90",

		_("Amount") + ":Currency:90",

	]

	return columns
```

This is not actually an IP address. It is a value used for formatting report columns. This is a false positive.

### File: erpnext/patches/v10_0/fichier_des_ecritures_comptables_for_france.py

#### Issue Detected by SonarQube

Add 1 missing arguments; 'install_country_fixtures' expects 2 positional arguments. The number and name of arguments passed to a function should match its parameters.

#### Analysis

```
def execute():
  frappe.reload_doc("regional", "report", "fichier_des_ecritures_comptables_[fec]")
for d in frappe.get_all("Company", filters={"country": "France"}):
  install_country_fixtures(d.name)
```

The install_country_fixtures function expects a second argument. There does not appear to be a security issue, but any incorrect code could be a reliability issue.

#### Mitigation

Since France is already identified, it appears that "France" should be passed as the second argument to install_country_fixtures.

### File: erpnext/stock/doctype/item/item.js

#### Issue Detected by SonarQube

Add a "return" statement to this callback.

#### Analysis

```
let selected_attributes = get_selected_attributes();
let lengths = [];
Object.keys(selected_attributes).map((key) => {
	lengths.push(selected_attributes[key].length);
});
```

No value is returned from the callback passed to map, so it returns an Array of undefined values. However, the return value of map is being ignored here and map is only being used to loop over the values of selected_attributes. There is no bug present, but the readability of the code could be improved.

#### Mitigation
```
let selected_attributes = get_selected_attributes();
let lengths = Object.values(selected_attributes).map((value) => {
	return value.length;
});
```

This code achieves the same result, but it actually uses the return values from map. It would prevent potential confusion about why the callback has no return value or why the result of map is ignored.

----

## Planned Contributions

We plan on reporting the issues in coupon_code.js and sales_partner.py. We have [this issue](https://github.com/CYBR-8420-Team-Open-Source-Elephant/ERPNext/issues/66) in our project to track this work.

----

## Team Reflection



