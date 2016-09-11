# jdlinker-parser
jdlinker-parser is a short python script that makes updating documentation projects that utilize sphinx-JDLinker much easier.

Since the core philosophy behind sphinx-JDLinker is that regular documentation editors shouldn't have to always download
the jars necessary to build their documentation project, and that JavaDoc jars shouldn't be hosted on the documentation
project itself, a tool is needed to ensure that all JavaDoc links that exist throughout the documentation are kept up-to-date.

## Minimum Requirements
The only two requirements are a `javadoc_dump.txt` file generated by sphinx-JDLinker, and the necessary **source** jars.

To get the `javadoc_dump.txt` file, navigate to your project's `conf.py` file, and set `javadoc_dump = True`. Run sphinx
at least once, and copy the generated dump file to another directory. This directory should also contain the `jdlinker_parser.py`
file.

Now you'll also need any necessary source jars in that same directory. For example, if I reference
```
:javadoc:`com.some.Foo`
```
in the documentation project, I'll need the Jar which contains Foo. Note that you do not need the Jar for method parameters.
For example, if I use
```
:javadoc:`com.some.Foo#someMethod(org.company.Bar)`
```
I would only need the jar which contains `com.some.Foo`.

## Using
Using jdlinker-parser is rather simple. Once you have:

- The `jdlinker-parser.py` file
- The `javadoc_dump.txt` file
- And the necessary source jars

in the same directory, you are ready to begin. You will need to execute the `jdlinker-parser.py` file passing in the source
jars as parameters. For example:
```
python jdlinker-parser.py my_jar-sources.jar my_other_jar-sources.jar
```

This will scan the `javadoc_dump.txt` file and inform you of what classes could not be found in either of those jars, as well
as what methods/fields could not be found in their respective files.
