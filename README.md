# pytest-start-from

A Pytest plugin to enable starting tests from a specified point.

## Use Case

You've got a test suite w/ 100s of tests. You run it with the `-x` option and
the 50th test fails. You make a small correction and want to run the suite
again, starting w/ the 50th test and proceeding to the end before starting over
and running tests 1 through 49.

## Usage

`py.test --start-from-file=path/to/file.py`

This option takes the list of tests pytest would run and "rotates" it so that
the tests in the specified file path are at the start of the list. For example
if your tests were in files a.py through z.py, and you specified n.py as the
argument here, this would result in tests n through z being run first, followed
by tests a through m.

Note that this option does not always provide exactly the results you expect.
If you have test methods decorated by some function that's defined elsewhere,
pytest may treat the path to the file defining the decorator as the path of the
test case. For this reason it may be more reliable to use the
`--start-from-test-case` option (see below).

`py.test --start-from-test-case=TestCaseClass.test_method_name`

This option works the same way as `--start-from-file`, but it identifies the
starting point by the actual test case itself rather than the path to the file
where that test case lives.
