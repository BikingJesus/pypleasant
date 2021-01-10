# pypleasant

*pypleasant* is a Python script and library which interfaces with
the [API](https://pleasantsolutions.com/info/pleasant-password-server/m-programmatic-access/restful-api) of
[Pleasant Password Server](https://www.passwordserver.de/).

```bash
pleasant-cli /path/to/entry --password  # print an entry's password
pleasant-cli /path/to/entry --attachments secret_file.txt  # download an attachment
pleasant-cli /path/to/entry --custom-field test  # print value of a custom field
```


## Requirements

pypleasant requires Python >= 3.6 and is only compatible with Pleasant Password Server
[API v5](https://pleasantsolutions.com/info/pleasant-password-server/m-programmatic-access/restful-api-v5).


## Installation

pypleasant is available on [PyPi](https://pypi.org/project/pypleasant/) and can be easily installed via pip:

```bash
pip install pypleasant
```

In order to use the command-line client `pleasant-cli`, ensure that your `PATH` variable includes
Python's `bin` directory (adapt if necessary):

```bash
export PATH+=$PATH:$HOME/.local/bin
```

Use the `--help` switch to check whether everything is setup correctly:

```bash
pleasant-cli --help
```

Alternatively, pypleasant can be executed as a Python module without modifying the `PATH` variable:

```bash
python -m pypleasant --help
```


## Configuration

`pleasant-cli` prompts the user for missing login information required for the Pleasant API.
This information can be configured (partially or completely) using command-line parameters
or environment variables:

* `--api-url` or `PLEASANT_API_URL`
* `--api-user` or `PLEASANT_API_USER`
* `--api-password` (**NOT RECOMMENDED**) or `PLEASANT_API_PASSWORD`

In case self-signed certificates are used, consider disabling the HTTPS certificate check via
`--disable-cert-check` or by setting `PLEASANT_DISABLE_CERT_CHECK=true`.


## Usage

Print entry attributes:

```bash
pleasant-cli /path/to/entry --username
pleasant-cli /path/to/entry --password
pleasant-cli /path/to/entry --url
```

Access a custom field's value:

```bash
pleasant-cli /path/to/entry --custom-field test
```

Download attachments (defaults to the current directory):

```bash
pleasant-cli /path/to/entry --attachments  # downloads all attachments
pleasant-cli /path/to/entry --attachments secret_file.txt
pleasant-cli /path/to/entry --attachments file_1.txt file_2.txt --download-dir /path/to/download/dir
```

For a complete overview of all parameters, run `pleasant-cli` with the `--help` switch:

```bash
> pleasant-cli --help
                       (--username | --password | --url | --custom-field [CUSTOM_FIELD] | --attachments [ATTACHMENTS [ATTACHMENTS ...]])
                       [--download-dir DOWNLOAD_DIR] [--api-url API_URL]
                       [--api-user API_USER] [--api-password API_PASSWORD]
                       [--disable-cert-check] [--verbose] [--debug]
                       path

positional arguments:
  path                  the path on the pleasant server to the credential
                        entry, e.g. /Development/git (env var:
                        PLEASANT_PATH_TO_ENTRY)

optional arguments:
  -h, --help            show this help message and exit
  --username            print the username
  --password            print the password
  --url                 print the URL
  --custom-field [CUSTOM_FIELD]
                        print the given custom field
  --attachments [ATTACHMENTS [ATTACHMENTS ...]]
                        download the given attachment(s); if no attachment is
                        given, all attachments are downloaded
  --download-dir DOWNLOAD_DIR
                        attachments are downloaded to this directory (DEFAULT:
                        '.', env var: PLEASANT_DOWNLOAD_DIR)
  --api-url API_URL     URL of the pleasant server api (env var:
                        PLEASANT_API_URL)
  --api-user API_USER   user for the pleasant server API (env var:
                        PLEASANT_API_USER)
  --api-password API_PASSWORD
                        password for the pleasant server API (env var:
                        PLEASANT_API_PASSWORD)
  --disable-cert-check  disable HTTPS cert check (env var:
                        PLEASANT_DISABLE_CERT_CHECK)
  --verbose             activate verbose output
  --debug               activate debug output (env var: PLEASANT_DEBUG)
```
