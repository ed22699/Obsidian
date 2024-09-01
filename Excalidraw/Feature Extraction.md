# <u>Control</u>
## Attributes
- `String[] FoldersPath`
- `Feature[] Feature` (where Feature is a enum) 
## Methods
- `void ExtractFeatures()`
# <u>Feature</u>
## Methods
- `String GetFeature(String ImagePath)`
# <u>Group Tool</u>
## Methods
- `List<String[]> Group(String[] FoldersPath)`
# <u>MetaData Editor</u>
## Attributes
- `List<String> Features`
## Methods
- `void WriteMetaData()`
- `void AddMetaData(String feature)`
- `void ViewMetaData()`