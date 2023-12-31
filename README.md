# Bencoding

Bencoding is a way to specify and organize data in a terse format. It supports the following types: byte strings, integers, lists, and dictionaries.

## Byte Strings
Byte strings are encoded as follows: `<string length encoded in base ten ASCII>:<string data>`

Note that there is no constant beginning delimiter, and no ending delimiter.

* Example: `4: spam` represents the string "spam" 

* Example: `0:` represents the empty string ""


## Integers
Integers are encoded as follows: `i <integer encoded in base ten ASCII> e`

The initial i and trailing e are beginning and ending delimiters.

* Example: `i3e` represents the integer "3"

* Example: `i-3e` represents the integer "-3"

`i-0e` is invalid. All encodings with a leading zero, such as i03e, are invalid, other than i0e, which of course corresponds to the integer "0".

NOTE: The maximum number of bit of this integer is unspecified, but to handle it as a signed 64bit integer is mandatory to handle "large files" aka .torrent for more that 4Gbyte.

## Lists
Lists are encoded as follows: `l <bencoded values> e`

The initial l and trailing e are beginning and ending delimiters. Lists may contain any bencoded type, including integers, strings, dictionaries, and even lists within other lists.

* Example: `l4:spam4:eggse` represents the list of two strings: [ "spam", "eggs" ] 

* Example: `le` represents an empty list: []


## Dictionaries
Dictionaries are encoded as follows: `d<bencoded string><bencoded element>e`

The initial d and trailing e are the beginning and ending delimiters. 

Note that the keys must be bencoded strings. 

The values may be any bencoded type, including integers, strings, lists, and other dictionaries. 

Keys must be strings and appear in sorted order (sorted as raw strings, not alphanumerics). 

The strings should be compared using a binary comparison, not a culture-specific "natural" comparison.

* Example: `d3:cow3:moo4:spam4:eggse `represents the dictionary { "cow" => "moo", "spam" => "eggs" } 

* Example: `d4:spaml1:a1:bee` represents the dictionary { "spam" => [ "a", "b" ] } 

* Example:` d9:publisher3:bob17:publisher-webpage15:www.example.com18:publisher.location4:homee` represents { "publisher" => "bob", "publisher-webpage" => "www.example.com", "publisher.location" => "home" } 

* Example: `de` represents an empty dictionary {}# Bencoding


## Tonight's Challenges


### 1. Serialise an object (Easier)

Given an object,  serialise it into the format as above.  For example

```
person = new {
    name: "David",
    age: 48
}

a = serialise(person)

print(a)

// 5:Davidi48e

```


### Ideas / Considerations

* Try to conform to the entire specification
* Support for NULL values
* Clear unit tests
* Performance


### 2. Deserialise an object (Harder)

Given an string,  use it to populate an object.  For example

```
class Person
{
    string name
    int age
}


person = deserialise("5:Davidi48e")

print(person.name)
// David

print(person.age)
// 48
 

```

### Ideas / Considerations

* Try to conform to the entire specification
* Clear and helpful error messages
* Support for NULL (optional) values (hard I think)
* Clear unit tests
* Performance



