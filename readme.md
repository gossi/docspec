# DocSpec
The docspec is a specification for an interoperable file format that documenting tools, like JavaDoc, can use. These tools normally work in 3 steps:

1. Parsing the code mapping docblocks to code
2. Generate an abstract format with the contents for the documentation
3. Generate the documentation

The docspec is the output of the second step. This would decouple the parsing step from the output step, so that these two things could be developed independently. With the goal that there will be a pool of various documenting tools and a pool of various display tools and that makes it easy for end users to combine them on their needs.

# Spec DRAFT - 2012-01-02
The docspec should be saved as JSON. Here is a first draft as a basis for discussion:

##ROOT
    {
		config: {
			name: "My cool library",
			url: "url to your documented product",
			version: "1.02-beta",
			description: DESCRIPTION,
			license: LICENSE,
			markup: "html|markdown" // defines which markup is used in the docblocks
			namespace: "namespace|package|module", // each language has its own 'type' of namespace that document display tools may layout different
			namespacedelimiter: ".|\"
			startswithnamespace: boolean, // like in php, root-namespaces start with the namespacedelimiter
			language: "javascript|php|coffeescript|java|perl|python|ruby|…" // for possible syntax highlighters :)
	    },
	    namespaces: [
			"mylib.widgets": {
				description: DESCRIPTION,
				see: [SEE, SEE, ..]
			},
			"mylib.viewers": {
				description: DESCRIPTION,
				see: [SEE, SEE, ..]
			},
			…
	    ],
		// files go here
	    "/path/to/file.ext": FILE,
	    "/path/to/another/file.ext": FILE,
	    …
    }

##FILE
	{
	    description: DESCRIPTION,
	    version: "$Id: 123 [..]$|0.9.5.2",
	    license: LICENSE,
	    authors: AUTHORS,
	    source: SOURCE,
	    variables: [VARIABLE, VARIABLE, ..],
	    constants: [VARIABLE, VARIABLE, ..],
	    classes: [CLASS, CLASS, ..],
	    interfaces: [INTERFACE, INTERFACE, ..],
	    traits: [TRAIT, TRAIT, ..],
	    functions: [FUNCTION, FUNCTION, ..]
	}

##VARIABLE
	"QNAME": {
	    COMMON,
	    type: TYPE
	}

##CLASS
	"QNAME": {
		COMMON,
		constructors: [FUNCTION, FUNCTION, ..], // constructors do have #constructor as name ?
		extends: [QNAME, QNAME, ..],
		implements: [QNAME, QNAME, ..],
		mixins: [QNAME, QNAME, ..]
		STRUCT_CONTENTS
	}

##INTERFACE
	"QNAME": {
		COMMON,
		extends: [QNAME, QNAME, ..],
		STRUCT_CONTENTS
	}

##TRAIT
	"QNAME": {
		COMMON,
		extends: [QNAME, QNAME, ..],
		mixins: [QNAME, QNAME, ..],
		STRUCT_CONTENTS
	}


##STRUCT_CONTENTS
{

	variables: [VARIABLE, VARIABLE, ..],
	constants: [VARIABLE, VARIABLE, ..],
	methods:  [FUNCTION, FUNCTION, ..]
}	

##FUNCTION
	"QNAME": {
		COMMON,
		returns: TYPE,
		params: [
			"name": {
				name: "name",
				type: TYPE,
				description: "A description with further details"
			},
			...
		],
		throws: [
			"QNAME": {
				name: "QNAME",
				description: "A description with further details"
			},
			...
		]
	}

##COMMON
{

	// identification
	name: "a name identifier"
	qname: QNAME,
	namespace: "a namespace identifier, this block belongs to",

	// description
	intro: "a short description, a oneliner",
	description: "a long description ",

	// visibility
	visibility: "private|protected|public|package",

	// modifiers
	static: boolean,
	abstract: boolean,

	// misc stuff
	since: "since when is this implemented",
	see: [SEE, SEE, ..],
	authors: [AUTHOR, AUTHOR, ..],
	source: SOURCE
}

##AUTHOR
	{
		name: "Thomas Gossmann",
		email: "myemail@myhost.com",
		url: "http://gos.si"
	}

##QNAME
The qualified unique name. Constructed after the following:

- STRUCT: namespace + config.namespacedelimiter + name
- FUNCTION: namespace + '#' + name
- METHOD: namespace + config.namespacedelimiter + STRUCT.name + '#' + name
  
Remark: If multiple functions/methods are present (due to operator overloading), they should get incremental suffixes, like #select-1, #select-2, same for constructors

##TYPE
Can either be a string or an object. 

### String
As a string this either represents a primitive type like "string", "boolean", "int", "float", "number", etc. or a QNAME. Squarebrackets [] as suffix identify, this type is an array. Multiple valid types can be listed and separated with the pipe character, like "int|mixed".

### Object
As an object, this type represents some form of an associative "config" object. This works like the following:

	{
		"name": TYPE,
		"name2": TYPE,
		...
	}



##SEE
Points to

- A QNAME rsp.
- The short version of QNAME, like #select which works within STRUCT and points to a method
- A url

##LICENSE
Can be

- Either a string indicating the used license, like "BSD", "LGPL", "GPLv3", etc. 
- a url to a license or
- a text with the license text passage

##DESCRIPTION
Basically a text, but can contain inline-tags, like: {@see SEE}

##SOURCE
The source (with stripped out docblocks?)





