# Contributing

## Set up the checkout

Clone the repository:

```sh
git clone https://codefloe.com/mcepl/rope-language-server.git
cd rope-language-server
```

Install the development dependencies using distribution packages, or use an
editable pip installation:

```sh
python3 -m pip install -e ".[all,websockets,test]"
```

The editable installation loads code from your checkout, so source changes do not
require reinstalling the package. Configure your editor to launch `rols`. Restart
its language-server process after changing code.

Without an editable installation, run `python3 -m rols` from the repository
directory to use the checkout directly.

Check the executable and enable logging when trying a change:

```sh
python3 -m rols --help
python3 -m rols -v --log-file /tmp/rols.log
```

The server waits for LSP messages over standard input. Launch it through your
editor when testing editor behaviour. Use `-vv` for debug logging.

## Run tests

```sh
python3 -m pytest
```

Useful pytest options:

- Run a specific file with `python3 -m pytest test/test_utils.py`.
- Run a specific function with `python3 -m pytest test/test_utils.py::test_debounce`.
- Match test names with `python3 -m pytest -k format`.
- Increase verbosity with `python3 -m pytest -v` or `python3 -m pytest -vv`.
- Enter a debugger on failure with `python3 -m pytest --pdb`.

For streamed cancellation tests and a headless Neovim check, see
[docs/cancellation-testing.md](docs/cancellation-testing.md).

## Format code and update configuration docs

Use the same Black version as CI:

```sh
python3 -m pip install black==25.11.0
python3 -m black --check .
```

Run `python3 -m black .` to apply formatting. Black is the development formatter;
this does not remove users' option to select Ruff for signature formatting.

After changing `rols/config/schema.json`, regenerate the configuration reference:

```sh
python3 scripts/jsonschema2md.py rols/config/schema.json CONFIGURATION.md
```
