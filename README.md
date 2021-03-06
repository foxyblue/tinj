<h1 align="center">
    Tinj
</h1>

<h4 align="center">
    Tinj adds a tinge of colour to newline delimited json streams on stdout.
</h4>

[![CircleCI](https://circleci.com/gh/foxyblue/tinj.svg?style=shield)](https://circleci.com/gh/foxyblue/tinj)

Perfect for JSON structured logs.

## Install

```bash
go get github.com/foxyblue/tinj
```

Ensure it has been installed correctly by running `tinj`
you should see the following output:

```bash
$ tinj
The command is intended to work with pipes.
Usage: cat file.json | tinj
```

## Usage

```bash
Usage:
  tinj [flags]
  tinj [command]

Available Commands:
  count       My counter
  help        Help about any command

Flags:
  -f, --format string      Supply a format string
  -h, --help               help for tinj
  -p, --separator string   Separate fields by supplied character
  -s, --style string       Supply a style of log such as [stern and compose]

Use "tinj [command] --help" for more information about a command.
```

Using docker-compose or [stern](https://github.com/wercker/stern)? Provide `--style` flag

```bash
# For stern logs
tinj --style stern

# For docker-compose logs
tinj --style compose
```

## Example

### Formatting JSON

From this 🧐

```bash
$ cat log_file.json
{"_id":"5d8557da792fb159ca70d568","index":0,"guid":"d83deabe-10cc-468d-9f92-e49b9c18c5fc","isActive":false,"balance":"$2,769.51","picture":"http://placehold.it/32x32","age":29,"eyeColor":"brown","name":"Hester Barron","gender":"male"}
{"_id":"5d8558182242931dbd4089c9","index":0,"guid":"6783e3bf-2901-4b34-966e-b5573b227e9b","isActive":true,"balance":"$3,254.41","picture":"http://placehold.it/32x32","age":40,"eyeColor":"brown","name":"Harvey Daniels","gender":"male"}
{"_id":"5d85582325447920d159e349","index":0,"guid":"a068825a-578a-40a7-ae35-861018a3c69b","isActive":true,"balance":"$1,439.11","picture":"http://placehold.it/32x32","age":22,"eyeColor":"brown","name":"Fischer Spencer","gender":"male"}
{"_id":"5d85582325447920d159e349","index":0,"guid":"a068825a-578a-40a7-ae35-861018a3c69b","isActive":true,"balance":"$1,439.11","picture":"http://placehold.it/32x32","age":22,"eyeColor":"brown","name":"Fischer Spencer","gender":"male"}
```

To this 🤩

```bash
$ cat log_file.json | tinj
5d8557da792fb159ca70d568 | Hester Barron | $2,769.51
5d8558182242931dbd4089c9 | Harvey Daniels | $3,254.41
5d85582325447920d159e349 | Fischer Spencer | $1,439.11
```

### Printing readable tracebacks

Formats JSON values with Newline Delimiters too.

```json
{"error":"\nErrorStatus: line 12\n    value not defined 'x'.\nSee docs for fix: sebastien-docs.info"}
```

Becomes:

```python
ErrorStatus: line 12
    value not defined 'x'.
See docs for fix: sebastien-docs.info
```

## Testing

```bash
go test ./...
```
