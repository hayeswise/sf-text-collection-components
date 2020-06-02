# sf-text-collection-components
Salesforce sub-flows related to text collections.

* Split
* Text Collection Includes
* Text Collection To String

# Components
## Split
Separates the input text into a collection of text values. The comma is the default separator. Optionally, a separator can be provided and it can a be text string such a semi-colon, one or more spaces, or a word, such as "and".

Inspired by the Java and Javascript split() method. Based on David Litton's "Parse Multi-Select" flow at https://salesforcesidekick.com/2016/11/07/parse-a-multi-select-value-in-visual-flow-unmanaged-package-included/.

### Input
* Text - Text - A delimted set of text values.
* Separator - Text. Optional. The character or text separating the values in the list. Extra spaces before or after the values will be ignored. The comma is the default separator. Optionally, a separator can be provided and it can a be text string such a semi-colon, one or more spaces, or a word, such as "and".

### Output
* Values - Text Collection.

## Text Collection Includes
Returns true if a text collection (array) contains the provided value; otherwise, returns false.

### Input
* Collection - Text Collection - A collection (array) of text values.
* Value - Text - The value to look for in the collection of text strings.

### Output
* IncludesValue - Boolean - True indicates that the value is a member of the collection; false indicates otherwise.

## Text Collection To String
Returns a Text collection (array) as a string (text) in the form of "[item1, item2, ...]".

### Input
* TextCollection - Text Collection.

### Output
* String - Text - A string representation of the TextCollection in the form of "[item1, item2, ...]".

# Installation
This is an unmanaged package.
Installation URL: https://login.salesforce.com/packaging/installPackage.apexp?p0=04t4T000001ptZk
