# ssp-parsing-tools

## Overview

Tools for turning existing SSP files into machine-readable formats.

### parsesheet

The `parsesheet` script writes the rows of a spreadsheet to a Sqlite database
and then collates the information by project and writes the output to a JSON file.

#### Usage

Currently the spreadsheets are hardcoded in the file and the database joins are specific to the spreadsheets. You will need spreadsheet files named `inventory.xlsx`, `implementation.xlsx`, and `tracking.xlsx`. Simply run the script and it will generate the JSON files in a directory named `projectjson/`. The files will be named using the project acronyms from the `implemenation.xlsx` file.

The spreadsheet should match the sqlite3 schema excluding the `id`:

```bash
sqlite> .schema
CREATE TABLE inventory (
	id INTEGER NOT NULL,
	production_operated_by TEXT,
	fips_199_overall_impact_rating TEXT,
	xlc_phase TEXT,
	date_authorization_memo_signed TEXT,
	date_authorization_memo_expires TEXT,
	information_system_or_program_name TEXT,
	acronym TEXT,
	authorization_boundary_description TEXT,
	uid TEXT,
	primary_operating_location TEXT,
	PRIMARY KEY (id)
);
CREATE TABLE tracking (
	id INTEGER NOT NULL,
	control_number TEXT,
	ars_baseline TEXT,
	control_type TEXT,
	control_name TEXT,
	control_set_version_number TEXT,
	authorization_package_name TEXT,
	allocation_status TEXT,
	overall_update_date TEXT,
	overall_control_status TEXT,
	assessment_status TEXT,
	tracking_id BIGINT,
	PRIMARY KEY (id)
);
CREATE TABLE implements (
	id INTEGER NOT NULL,
	information_system_or_program_name TEXT,
	acronym TEXT,
	primary_operating_location TEXT,
	control_number TEXT,
	shared_implementation_details TEXT,
	private_implementation_details TEXT,
	tracking_id TEXT,
	PRIMARY KEY (id)
);
```
