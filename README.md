Download Link: https://assignmentchef.com/product/solved-homework-4-data-extraction-conversion-sorting-and-build-a-csv-file-output-cop3502-cs-1
<br>
As discussed in <em>Homework 3 </em>many ETL (extraction, transformation, and loading) problems parse data files wherein the data fields is separated by commas and data is converted from one format to another. This assignment is a continuation of that process – with an additional two steps. The first step is to sort the airports alphabetically. The second step is to sort the airports geographically and plan a route from south to north, all the while flying over land.

This assignment requires the data extraction, degree conversion, data formatting, sorting by two different criteria, and output the sorted results. The file inputs are defined in the <em>Inputs</em>. Similarly, the sort criteria are defined in <em>Processes </em>and the outputs are defined in <em>Outputs</em>.

<h1>1          Objectives</h1>

The objectives of this assignment are to demonstrate proficiency in file I/O, data structures, data transformation, sorting techniques, and file output using C language resources.

<h1>2          Inputs</h1>

There are two basic inputs, the input file name, passed via the command line, and the input file data sort order defined below.

<h2>2.1        Command Line arguments</h2>

The input file name will be input as follows:

<ul>

 <li>hw4Sort filename.ext sortParameter</li>

 <li>In the event that the input file is not available or there is an error finding the file, an appropriate error message shall be displayed. Use the example below for guidance.</li>

 <li>hw4Sort ERROR: File “bogusFilename” not found.</li>

 <li>In the event that the sortParameter is not available, an appropriate error message shall be displayed. Use the example below for guidance.</li>

 <li>hw4Sort ERROR: sortParameter invalid or not found.</li>

 <li>It would be appropriate to display the valid sort parameters in the error message. The <em>valid </em>sort parameters are a for <em>alphabetical sort </em>or n for <em>North Bound Exit</em>. The sort parameters can be entered in either upper or lower case.</li>

</ul>

<h2>2.2        Input File fields</h2>

The CSV input file contains the following fields. Please note these fields may vary in size, content, and validity of the data. Also note that some of the data formats are a <em>melange </em>of types. Specifically, note that both latitude and longitude contain numbers, punctuation, and text. Likewise, the FAA Site number contains digits, letters, and punctuation. (<em>This assignment will treat all input data as character data. Additional</em>

<em>conversions are specified later in Processes.</em>)

Table 1: Airports Data Fields

<table width="432">

 <tbody>

  <tr>

   <td width="136">Field Title</td>

   <td width="167">Description</td>

   <td width="129">Size</td>

  </tr>

  <tr>

   <td width="136">FAA Site Number</td>

   <td width="167">Contains leading digits followed by a decimal point and short text</td>

   <td width="129">Leading digits followed by a decimal point and zero to two digits and a letter</td>

  </tr>

  <tr>

   <td width="136">Loc ID</td>

   <td width="167">The airport’s short name, i.e.MCO for Orlando</td>

   <td width="129">4 characters</td>

  </tr>

  <tr>

   <td width="136">Airport Name</td>

   <td width="167">The airport’s full name, i.e.Orlando International</td>

   <td width="129">~30 characters</td>

  </tr>

  <tr>

   <td width="136">Associated City</td>

   <td width="167">The nearest city</td>

   <td width="129">~25 characters</td>

  </tr>

  <tr>

   <td width="136">State</td>

   <td width="167">State</td>

   <td width="129">2 characters</td>

  </tr>

  <tr>

   <td width="136">Region</td>

   <td width="167">FAA Region</td>

   <td width="129">3 characters</td>

  </tr>

  <tr>

   <td width="136">ADO</td>

   <td width="167">Airline Dispatch Office</td>

   <td width="129">3 characters</td>

  </tr>

  <tr>

   <td width="136">Use</td>

   <td width="167">Public or Private</td>

   <td width="129">2 characters</td>

  </tr>

  <tr>

   <td width="136">Latitude</td>

   <td width="167">DD-MM-SS.MASDirection</td>

   <td width="129">Degrees, minutes, seconds,                milliarcseconds followed by either N or S.</td>

  </tr>

  <tr>

   <td width="136">Longitude</td>

   <td width="167">DD-MM-SS.MASDirection</td>

   <td width="129">Degrees, minutes, seconds, milliarcseconds followed by either E or W.</td>

  </tr>

  <tr>

   <td width="136">Airport Ownership</td>

   <td width="167">Public or Private</td>

   <td width="129">2 characters</td>

  </tr>

  <tr>

   <td width="136">Part 139</td>

   <td width="167">FAA Regulation</td>

   <td width="129">No data</td>

  </tr>

  <tr>

   <td width="136">NPIAS Service Level</td>

   <td width="167">National     Plan  IntegratedAirport Systems Descriptor</td>

   <td width="129">~10 characters</td>

  </tr>

  <tr>

   <td width="136">NPIAS Hub Type</td>

   <td width="167">Intentionally left blank</td>

   <td width="129">n/a</td>

  </tr>

  <tr>

   <td width="136">Airport Control Tower</td>

   <td width="167">Y/N</td>

   <td width="129">one character</td>

  </tr>

  <tr>

   <td width="136">Fuel</td>

   <td width="167">Fuel types available</td>

   <td width="129">up to 6 characters</td>

  </tr>

  <tr>

   <td width="136">Other Services</td>

   <td width="167">Collections of tag indicating INSTRuction, etc.</td>

   <td width="129">12 characters</td>

  </tr>

  <tr>

   <td width="136">Based Aircraft Total</td>

   <td width="167">Number of aircraft (may be blank)</td>

   <td width="129">Integer number</td>

  </tr>

  <tr>

   <td width="136">Total Operations</td>

   <td width="167">Takeoffs/Landings/etc (may be blank)</td>

   <td width="129">Integer number</td>

  </tr>

 </tbody>

</table>

<h1>3          Processes</h1>

The primary goal is to provide programmatic access to the data from the input CSV file. This must be accomplished using standard C file IO techniques. Also note that it is vital to utilize the <em>stuct airPdata </em>for all data retrieval/extraction and conversion. Likewise, use of the <em>stuct airPdata </em>is required for the file output.

<h2>3.1        Reading the input</h2>

There are several approaches to read the input. Perhaps the most important consideration is reading the line in for each airport. Please note that there is one line per airport. Also note, that once the line is read into the input buffer it might be advantageous to parse the input buffer based on the <em>comma </em>delimiter.

There are several approaches possible. Make sure to test on <em>Eustis </em>as line termination characters/behaviors vary amongst operating systems.

<em>Make sure that the output file is formatted with decimal degrees.</em>

<h2>3.2        Processing the data structure</h2>

The data conversions for this assignment, specified below, require a certain degree of parsing and calculation. Initially reading the input is to your advantage to deal with all data elements as <em>character data</em>. And then process the <em>latitude </em>and <em>longitude</em>, hereinafter referred to as <em>degrees</em>. The <em>degrees </em>are expressed as <em>sexagesimal (base 60) </em>numbers. Therefore use the functions created in <em>Homework 3 </em>to establish <em>valid </em>latitudes and longitudes.

Please note that there are some airports whose <em>Loc ID </em>begin with numerical digits. There are also quite a few that contain two trailing digits. Typically these are helipads. For the purposes of this assignment those <em>airports </em>can be ignored or discarded from the input. <em>Careful review of these airports will reveal they typically start with the string FL or X and are followed by 2 digits.</em>

Once the input data has been appropriately extracted and converted, save it in memory in a <em>singly linked list</em>. This will facilitate further processing.

<h3>3.2.1       Latitude/Longitude Input</h3>

The <em>latitude </em>and <em>longitude </em>are both degrees, expressed as shown in the table below.

The conversion of the DDD-MM-SS.MASD string is shown in Table 2. The formula to convert a <em>sexagesimal </em>degree measurement to a digital degree measurement is shown below.

<em>degrees<sup>decimal </sup></em>=±<em>DDD </em>+ <em>MM/</em>60+ <em>SS.MAS/</em>60<sup>2</sup>

Table 2: Degrees

<table width="416">

 <tbody>

  <tr>

   <td width="79">Placeholder</td>

   <td width="154">Name</td>

   <td width="92">Value</td>

   <td width="92">Decimal</td>

  </tr>

  <tr>

   <td width="79">DD</td>

   <td width="154">Degrees</td>

   <td width="92">180</td>

   <td width="92">0-180</td>

  </tr>

  <tr>

   <td width="79">MM</td>

   <td width="154">Minutes</td>

   <td width="92">0-59</td>

   <td width="92"><em><u>value </u></em>60</td>

  </tr>

  <tr>

   <td width="79">SS.MAS</td>

   <td width="154">Seconds.MilliArcSeconds</td>

   <td width="92">0-59.0-9999</td>

   <td width="92"><em><u>value </u></em>60<sup>2</sup></td>

  </tr>

  <tr>

   <td width="79">D</td>

   <td width="154">Direction</td>

   <td width="92">N,S,E,W</td>

   <td width="92">See Table 3</td>

  </tr>

 </tbody>

</table>

Table 3: Direction

<table width="207">

 <tbody>

  <tr>

   <td width="71">Unit</td>

   <td width="48">Name</td>

   <td width="89">Decimal Sign</td>

  </tr>

  <tr>

   <td width="71">Latitude</td>

   <td width="48">NS</td>

   <td width="89">+–</td>

  </tr>

  <tr>

   <td width="71">Longitude</td>

   <td width="48">EW</td>

   <td width="89">+–</td>

  </tr>

 </tbody>

</table>

Note that the ± is derived from the information in Table 3 above.

<h2>3.3        Functions</h2>

<h3>3.3.1       float sexag2decimal(char *degreeString);</h3>

Description: Convert the <em>sexagesimal </em>input string of <em>chars </em>to a decimal degree based on the formula in Tables 2 and 3.

Special Cases: If a NULL pointer is passed to this function, simply return 0.0. Similarly, if the DD-MM-SS.MASD fields have invalid or out-of-range data, return

0.0.

Caveat: Even though the <em>valid </em>range of Degrees is from 0 to 180, the data files for the Continental US and Florida are from 0 to 99. Make sure that the conversion can handle all valid cases correctly.

Hint: Take care to make sure the values for each numeric component are within their valid ranges. Refer to Table 2 for the ranges.

Returns: A floating point representation of the calculated <em>decimal degrees </em>or 0.0 in the special cases mentioned above.

<h3>3.3.2       void sortByLocID(lListAirPdata *airports);</h3>

Description: Sorts the airports <em>alphabetically </em>by the string named <em>Loc ID </em>with only one airport per letter. That is the first airport to begin with a <em>Loc ID </em>starting

with the letter A would be the <em>only </em>airport beginning with the letter A. Increments the <em>seqNumber </em>as each airport is updated as a selected output.

Special Cases: Remember the helipads! In other words, it is acceptable to skip airports whose <em>Loc ID </em>begin with a number, or start with either FL or X followed by two digits.

Caveat: Since the sorting options are mutually exclusive, this function can destructively manipulate the input list to produce the desired results.

Hint: It might be faster to use the <em>Loc ID </em>as a hash value or perhaps as an index into an array, after all, there can only be one airport per letter of the alphabet.

Returns: Nothing. However the input data should be seriously modified by this process.

<h3>3.3.3       void sortByLatitude(lListAirPdata *airports);</h3>

Description: Sorts the airports by <em>latitude </em>from South to <em>North</em>. Think of this as an <em>Escape from Key West to Georgia</em>.

Increments the <em>seqNumber </em>as each airport is updated as a selected output.

Special Cases: Remember the helipads! In other words, it is acceptable to skip airports whose <em>Loc ID </em>begin with a number, or start with either FL or X followed by two digits.

Output: Output the airports’ data per the <em>output file specification </em>derived from walking thru the <em>AVL </em>tree until reaching the maximum latitude for the Florida border. <em>For the purposed of this exercise, assume 31 degrees North.</em>

Caveat: Since the sorting options are mutually exclusive, this function can destructively manipulate the input list to produce the desired results.

Hint: It might be faster to use the <em>Latitude </em>as a measurement criteria for building an <em>AVL </em>tree.

Returns: Nothing. However the input data should be seriously modified by this process.

<h1>4          Outputs</h1>

The outputs of the program will be populated Struct airPdata data. This data will be formatted so as to provide output as defined in the following sections.

<h2>4.1        Data Structures</h2>

<h3>4.1.1       struct airPdata</h3>

The structure struct airPdata is described below. Please note the correlation with the data file’s <em>Field Names </em>refer to Table 1 on page 3 for more information.

typedef struct airPdata{

int seqNumber; //The process output’s sequence number char *LocID;          //Airport’s ‘‘Short Name’’, ie MCO char *fieldName; //Airport Name char *city; //Associated City float longitude; //Longitude float latitude; //Latitude

} airPdata;

<h3>4.1.2       linked list of airPdata</h3>

typedef struct lListAirPdata{

airPdata *curAirPdataP;      //Pointer to the Airport Data lListAirPdata *nextAirPdataList; // pointer to next

} lListAirPdata;

<h2>4.2        File output</h2>

The file output for this assignment is <em>stdout</em>, aka the console. Make sure there is a headline that names each column. For example:

seqNumber,code,name,city,lat,lon

1,DAB,DAYTONA BEACH INTL,DAYTONA BEACH,29.1797,-81.0581

2,FLL,FORT LAUDERDALE/HOLLYWOOD INTL,FORT LAUDERDALE,26.0717,-80.1494

3,GNV,GAINESVILLE RGNL,GAINESVILLE,29.6900,-82.2717

4,JAX,JACKSONVILLE INTL,JACKSONVILLE,30.4939,-81.6878

5,EYW,KEY WEST INTL,KEY WEST,24.5561,-81.7594

6,LAL,LAKELAND LINDER RGNL,LAKELAND,27.9889,-82.0183

7,MLB,MELBOURNE INTL,MELBOURNE,28.1025,-80.6450

8,MIA,MIAMI INTL,MIAMI,25.7953,-80.2900

9,APF,NAPLES MUNI,NAPLES,26.1522,-81.7756

10,SGJ,NORTHEAST FLORIDA RGNL,ST AUGUSTINE,29.9592,-81.3397

11,ECP,NORTHWEST FLORIDA BEACHES INTL,PANAMA CITY,30.3581,-85.7956

12,OCF,OCALA INTL-JIM TAYLOR FIELD,OCALA,29.1717,-82.2239

13,MCO,ORLANDO INTL,ORLANDO,28.4292,-81.3089

Things to note:

<ul>

 <li>The sample output above is an example only.</li>

 <li>Digital degrees are expressed as floating point numbers of varying digits of precision. This is an artifact of <em>Javascript</em>. In this exercise 4 digits to the right of the decimal point is sufficient.</li>

 <li>The first line of the file identifies the field names. This is a material fact and will adversely impact the output of the data in the webpage. <em>Capitalization and spelling matter – and must match the first line above.</em></li>

 <li>The text shown above has been converted to uppercase as a piece of information to help debugging. String case conversion is not required for this exercise.</li>

</ul>

Once the output has been verified, redirect the <em>stdout </em>to a file named myTestAirports.csv. Make sure that all code, inputs, and outputs are built, tested, and the output file is exported from <em>Eustis</em>.

<h2>4.3        Testing</h2>

There is one input file provided for program testing. It is described below. The pro-

Table 4: Test Files

<table width="370">

 <tbody>

  <tr>

   <td width="128">Filename</td>

   <td width="243">Description</td>

  </tr>

  <tr>

   <td width="128">FL-ALL-airports.csv</td>

   <td width="243">A list of the <em>875 </em>Florida airports, wherein all the data is formatted as defined in the Input Specification.</td>

  </tr>

 </tbody>

</table>

gram’s output will be to <em>stdout</em>. Redirect the output to the file named <em>myAirports.csv</em>.