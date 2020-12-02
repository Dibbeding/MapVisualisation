How to make the dataset ready:

NECESSARY:
 - Only keep columns for "Year, Area, Code"
 - Sort colums first by 'Year', then by 'Area'
 - Check for countries that have had name changes:
   * Czechoslovakia => Czechia
   * Ethiopia PDR   => Ethiopia
   * USSR           => Russia
   * Yugoslav SFR   => 

OPTIONAL:
 - Optional? Remove Countries with multiple null-entries in the same year
 - Remove regions that are not (single) countries or that don't exist anymore:
   * Belgium-Luxembourg
   * Pacific Islands Trust Territory


CHANGED NAMES:
There are some name-related problems with the geoJSON-data and the FAOSTAT-data.
The left columns are from the geoJSON-data, the right columns are from the FAOSTAT-data

These names are different between the two files:
- United States        = United States of America
- Russia               = Russian Federation
- Dominican Rep.       = Dominican Republic
- Venezuela            = Venezuela (Bolivarian Republic of)
- Bolivia              = Bolivia (Plurinational State of)
- Central African Rep. = Central African Republic
- Eq. Guinea           = Equatorial Guinea
- S. Sudan             = South Sudan
- Dem. Rep. Congo      = Democratic Republic of the Congo
- Swaziland            = Eswatini
- Tanzania             = United Republic of Tanzania
- Syria                = Syrian Arab Republic
- Iran                 = Iran (Islamic Republic of)
- Moldova              = Republic of Moldova
- Macedonia            = North Macedonia
- Bosnia and Herz.     = Bosnia and Herzegovina
- Czech Rep.           = Czechia
- United Kingdom       = United Kingdom of Great Britain and Northern Ireland
- Dem. Rep. Korea      = Democratic People's Republic of Korea
- Korea                = Republic of Korea
- Vietnam              = Viet Nam
- Lao PDR              = Lao People's Democratic Republic
- Brunei               = Brunei Darussalam
- Solomon Is.          = Solomon Islands

These countries don't have FAOSTAT-data:
- Greenland            = ---
- W. Sahara            = ---
- Djibouti             = ---

These countries are considerd part of another country in the FAOSTAT-data, but separte in the geoJSON:
- N. Cyprus            = Cyprus
- Somaliland           = Somalia 
- Taiwan               = China

* For filter and sort, make the animal type (subject) selectable with all options from FAOSTAT, but only the chicken one is needed and shows the correct dataset for the subject
* Also years selectable on filter and sort.