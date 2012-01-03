# DocSpec
The docspec is a specification for an interoperable file format that documenting tools, like JavaDoc, can use. These tools normally work in 3 steps:

1. Parsing the code mapping docblocks to code
2. Generate an abstract format with the contents for the documentation
3. Generate the documentation

The docspec is the output of the second step. This would decouple the parsing step from the output step, so that these two things could be developed independently. With the goal that there will be a pool of various documenting tools and a pool of various display tools and that makes it easy for end users to combine them on their needs.

## Goto
- [See the Spec](https://github.com/gossi/docspec/blob/master/spec.md)
- [Check out the Example](https://github.com/gossi/docspec/blob/master/example.json)
- [Discuss using Github's issues feature](https://github.com/gossi/docspec/issues)

## Participating Doctools
none yet, yay this is totally new. If you are a doctool author and have interesst in implementing the docspec, feel free to fork this file and add yourself.

- [phpdoctor](https://github.com/peej/phpdoctor) [Language: PHP]  
  See issue: https://github.com/peej/phpdoctor/issues/58

## History
2012-01-02 Created first draft version

## Resources
- [My Blog Post](http://gos.si/blog/docspec-as-interoperable-file-format-between-doctools)
- [PSR](https://github.com/docblox/docblox/blob/master/docs/PSR.md) (PSR = PHP Standards RFC, it is a form of RFC for the PHP Standards Group)  
  Demo at: http://demo.docblox-project.org/default/structure.xml







