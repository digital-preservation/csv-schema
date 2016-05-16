CSV Schemas
===========

CSV Schemas expressed in the [CSV Schema Language](http://digital-preservation.github.io/csv-schema/csv-schema-1.1.html).


Digital Preservation @ TNA
--------------------------

CSV Schema created by the Digital Preservation and Digital Repository Infrastructure teams at The National Archives will be added to this folder to make them available to digitisation partners and to serve as examples of the use of the CSV Schema Language.

An initial example CSV can be found in the \[`example-data`\](http://github.com/digital-preservation/csv-schema/tree/master/example-schemas/example-data) folder, which relates to the xml files to be found in its subfolder TEST_1 and further subfolders.  This is designed to be validated against the schema \[`digitised_surrogate_tech_acq_metadata_v1_TESTBATCH000.csvs`\](https://github.com/digital-preservation/csv-schema/blob/master/example-schemas/digitised_surrogate_tech_acq_metadata_v1_TESTBATCH000.csvs).  In a genuine digitisation project, the files described by the metadata CSV would be JPEG2000s, but these would tend to be quite large, so to make downloading more practical for demonstration purposes, we have supplied only the XML which would normally be embedded within the JPEG2000 file.


Other
-----

`TCP.csvs` CSV Schema provided for validation of Early English Texts released by the TEI project.

Regex
-----

Various regex have been reused between different schemas at TNA, for ready reference some are reproduced here

Surname checking (this comes with a health warning, it will show that a string looks something like a "British/European" surname, 
it does not attempt to claim it will correct validate all names, especially those from non-European cultures.  It has limited Unicode awareness to cater for accented characters

```
^(((([dDL][\?aeiou]([- ]?))|([dDAL](e)?\')|([dD]e([- ]?)[lL]a([- ]?))|(St(e?[- ]?))|([Vv][\?ao]n( ?)([Dd]e[rn]?( ?))?))|(M[\?a]?[\?c]|M\'|O\'))?[\?A-Z][\?\p{Ll}]{2,15})(([- ])((([dDL][\?aeiou]([- ]?))|([dDAL](e)?\')|([dD]e([- ]?)[lL]a([- ]?))|(St(e?[- ]?))|([Vv][\?ao]n( ?)([Dd]e[rn]?( ?))?))|(M[\?a]?[\?c]|M\'|O\'))?[\?A-Z][\?\p{Ll}]{2,15})?$
```

Forename checking

```
^((St(e?[- ]?))|(M[\?a]?[\?c]|M\'))?[\?A-Z][\?\p{Ll}]{2,15}([- ](((([dDL][\?aeiou]([- ]?))|([dDAL](e)?\')|([dD]e([- ]?)[lL]a([- ]?))|(St(e?[- ]?))|([Vv][\?ao]n( ?)([Dd]e[rn]?( ?))?))|(M[\?a]?[\?c]|M\'|O\'))?[\?A-Z][\?\p{Ll}]{0,15}))*$
```

While these look complex they break down into a few simpler blocks:
```((([dDL][\?aeiou]([- ]?))|([dDAL](e)?\')|([dD]e([- ]?)[lL]a([- ]?))|(St(e?[- ]?))|([Vv][\?ao]n( ?)([Dd]e[rn]?( ?))?))|(M[\?a]?[\?c]|M\'|O\'))?``` defines "particles" that may appear
at the start of names and might cause a name to begin with a lower case letter which would otherwise be unexpected, this is things like de, de la, St, Mac etc, then
```[\?A-Z][\?\p{Ll}]{2,15}``` says that we expect the main part of the name to start with a capital letter and be followed by at least two lower case letters (\p{Ll} is unicode aware to allow 
accented characters.  We then allow repeats of these basic building blocks, separated by either hyphen or space to allow for multiple forenames, or multi-barrelled surnames.
The version used in forenames allows subsequent forenames to be expressed as initials only, but as many repoeats as needed, while in surnames the regex as written allows only 2 barrels in
total, additional ones could be allowed be changing the final question mark to {0,2} for 3 barrels in total etc.

A more generic check would be ``````regex("^([- \'\?\p{Ll}\p{Lu}\]*|\*]$")``` requiring one or more characters from the set specified, hyphen, space, apostrophe, question mark (for unreadable characters), upper or lower case characters (as defined in Unicode), or a single asterisk (representing a blank entry).

Titles/postnominals

Again this is not complete, and does not currently recognise every postnominal that might occur in the British honours system, and certainly does not attempt to enforce the correct order of precedence
It was first used in a project where both "titles" and postnominals were actually transcribed after the intials given for a record subject

```
((((The )?Rev)|Sir|MA|BA|DD|BD|MB|Bart|VC|[GK]?CB|[GK]?CMG|[GK]?CVO|DSO|DSC|MC|DSM|DCM|[OM]BE|BEM|ADC|Mrs|Miss|Capt|Major|CDR|RM)( (((The )?Rev)|Sir|MA|BA|DD|BD|MB|Bart|VC|[GK]?CB|[GK]?CMG|[GK]?CVO|DSO|DSC|MC|DSM|DCM|[OM]BE|BEM|ADC|Mrs|Miss|Capt|Major|CDR|RM))*
```
