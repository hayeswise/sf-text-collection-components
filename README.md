# sf-text-collection-components
The Text Collection Components package contains Salesforce sub-flows related to text collections.

* Split
* Text Collection Includes
* Text Collection To String

## Motivation
I developed these to support a custom Salesforce app for the [John Muir Land Trust](https://www.jmlt.org) membership program.  The NPSP Mebership solution did not meet the needs since it was based on tracking a single donation rather than tracking cumulative donations within a qualifying period (typically a calendar year).

The `Split` subflow is used to convert a comma separated list of Opportunity Record Type names into a text collection.  This list represents the record types that are in scope.  For example, Donation, Gala, and Grant are in scope (among others).  Orignially, I used the resultant collection to lookup the Opporunity Record Type Ids which were then used in the Get Records condition.  

However, with improvements in the [UnofficialSF](https://unofficialsf.com/)'s [Excecute SOQL Action](https://unofficialsf.com/a-graphical-soql-query-builder-for-flow/), I simplified the get-account-and-contact-oppportunities flow to use the `Execute SOQL` action. With this I could use the `SOQL WHERE...IN` clause to filter on the Record Type names.  This required the names needed to be single quoted. Since I didn't want to burden the admin with doing this in the configuration record (a metadata object), I passed the output of the `Split` into the `Text Collection To String` with appropriate `Bracket` and `Quote` parameter values.  In this way, a text template for building the SOQL could do something like this:

```
..." AND RecordType.Name IN (" & {!InScopeOpportunityRecordTypeNames} & ")"
```


# Components
## Split
<img align="right" src="https://github.com/hayeswise/sf-text-collection-components/blob/master/images/Split.png">

Separates the input text into a collection of text values. The comma is the default separator. Optionally, a separator can be provided and it can a be text string such a semi-colon, one or more spaces, or a word, such as "and".

Inspired by the Java and Javascript split() method. Based on David Litton's "Parse Multi-Select" flow at https://salesforcesidekick.com/2016/11/07/parse-a-multi-select-value-in-visual-flow-unmanaged-package-included/.

### Input

| Parameter | Type | Description|
| :-- | :-- | :-- |
| Text | Text | A delimted set of text values. |
| Separator | Text | Optional. The character or text separating the values in the list. Extra spaces before or after the values will be trimmed (removed). The comma is the default separator. Optionally, a separator can be provided and it can a be text string such a semi-colon, one or more spaces, or a word, such as "and".|

### Output
| Parameter | Type | Description|
| :-- | :-- | :-- |
| Values | Text Collection | A text collection (array) of the values in the input Text. |

## Text Collection Includes
<img align="right" src="https://github.com/hayeswise/sf-text-collection-components/blob/master/images/TextColllectionIncludes.png">
Returns true if a text collection (array) contains the provided value; otherwise, returns false.

### Input

| Parameter | Type | Description|
| :-- | :-- | :-- |
| Collection | Text Collection | A collection (array) of text values. |
| Value | Text | The value to look for in the collection of text strings. |

### Output

| Parameter | Type | Description|
| :-- | :-- | :-- |
| IncludesValue | Boolean | True indicates that the value is a member of the collection; false indicates otherwise. |

## Text Collection To String
<img align="right" src="https://github.com/hayeswise/sf-text-collection-components/blob/master/images/TextCollectionToString.png">
Returns a Text collection (array) as a comma separated string of values.  The default format is "[value1,value2,...]". The enclosing brackets can be suppressed and the the individual values can be quoted to give you a string in the format of "'value1','value2',..."


### Input

| Parameter | Type | Description|
| :-- | :-- | :-- |
| Collection | Text Collection | A text collection (array) |
| Braket | Boolean | If true, the returned string starts with an opening bracket and ends with a closing bracket; otherwise, brackets are not added. Default value is true. |
| Quote | Text | Set to a quote character, such as the single quote or double quote, to prepend and append to each item. Defaults to empty string. Useful for creating lists for a SOQL WHERE...IN clause. |

### Output

| Parameter | Type | Description|
| :-- | :-- | :-- |
| String | Text | A string representation of the TextCollection. If default values are provided for Braket and Quote, String will be in the form of "[item1, item2, ...]". |

# Installation
This is an unmanaged package.

Installation URL: https://login.salesforce.com/packaging/installPackage.apexp?p0=04t4T000001ptaT

Installation URL path and search part: packaging/installPackage.apexp?p0=04t4T000001ptaT

