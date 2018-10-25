## Updating Red Cross CARTO Diaspora Mapping Tool

This is a readme for adding additional information to the Red Cross diaspora mapping tool. It
covers all the types of data that may need to be inserted. The two main types of information
that are anticipated to be added are additional resources for the resource tab, and adding an
additional population group. The second operation is fairly complicated and time-intensive.

### 1. Updating the Resources Tab:

Updating the resources tab requires adding a row with the information for the additional
embassy or community resource you wish to add to the document. There are a wide variety of
resources for each diaspora group that are not included in the map, and finding them is
accomplished through a relatively easy google search. Once the resource is identified, its
information can be inserted into the CARTO online resources database. Once it is added to
the data sheet, it will be included in the resources map. Inserting a row is as simple as going
to the data sources tab and clicking the embassies_resources_v3 data set. Once the data set
is open, click the insert-row button and fill out the information for the additional resource. It is
very important to ensure that all of the columns are filled out for the additional data, especially
the coordinates column. To find the coordinates for the additional resource you are adding,
use a tool like https://www.gps-coordinates.net/. For reference: Latitude = Y, Longitude = X.

### 2 and 3: Adding a new population map (More Difficult):

Adding countries to the tool is a bit more difficult. It requires basic HTML knowledge,
management of large datasets, and familiarity with the CARTO system. Updating it can be
broke into two parts: adding an additional tab to the website, and adding an additional map to
the CARTO library.

In order to create a new tab with an additional population group, four steps must be taken.
The first (2A) is to create a new dataset with your population. The second (2B) is to upload
the place data and create a map featuring the population, in the same stye as the previous
maps. The final step (2C) is to include the state-level layer and the fire data layer. Finally, in
step 3, the HTML tabs can be updated and the whole application can be packaged.

### 2A. Uploading your new population data

To begin, data featuring the new population must be uploaded to CARTO. This requires
pulling the data from the same source – the American Community Survey 2016 5-Year Place
Data. This data is divided by metropolitan area, and the ACS_FBC_2016 data sheet on the
RedCross CARTO page already features these locations geocoded. Therefor, the easiest
way of inserting new population data is to download this data sheet as a copy, and to add the
additional column with the new populations data. This data can be pulled from the ACS
database using excel, SQL, or any preferred method for extracting data columns. The ACS
database can be requested from the RedCross, or it can be downloaded from the ACS
website directly. For reference, the correct database is called ACS_2016_5YR_PLACE.gdb.
The column with the data inside of the database can be joined to the ACS_FBC_2016 copy
sheet you have downloaded by joining the columns identifying the unique ID of each place –
placefp. Create a new sheet combining all the data, and remove unnecessary columns (ones
that are not featured in the template you have downloaded from CARTO.) Once the duplicate
columns have been removed, rename the column featuring your new populations data after
the country that population is focused on.

This newly created data table should be fairly large, and should be uploaded to the
RedCrosses CARTO page. Use a name that indicates the file is a modified copy – e.g.
ACS_FBC_2016_Copy_Burkina The above described section is the most complex part of the
process, and may require some trial and error depending on any issues encountered with the
data. This also requires manipulating very large files and may not be possible on older
computers.

Follow the same steps as above for the State data. The source for the state data comes from
the American community survey as well. The data from the ACS_2016_5YR_PLACE.gdb can
be simplified by state by sorting the information by state code – labeled at statefp. Create a
new table with the sum of the population for each state, and join that with a copy of
ACS_FBC_STATE from the RedCross CARTO site. The columns to be joined are called
statefp.

The next step is creating the CARTO Map with the data.

### 2B. Creating a map on CARTO with the place data

The map should be created to match the other, already functioning CARTO maps. This is
best accomplished by using one of them as a template. Once the template is open, rename it
as a different map indicating which diaspora group you are highlighting. Select the dataset
featuring your population group for the first layer. This should reset the whole map, and each
stylizing option will need to be reselected. The most straightforward way to do this is to enter
CSS codes, and switch out the name of the column indicating each country for the name of
the column indicating your populations data set.

See Below:

**style**
```
#layer {
  marker-line-width: 1;
  marker-line-color: #ffffff;
  marker-line-opacity: 0;
  marker-width: ramp([your_population_column_name], range(0, 30), headtails(7));
  marker-fll: #eb2135;
  marker-fll-opacity: 0.9;
  marker-allow-overlap: true;
}
```

**Popup (Click)**
```
<div class="CDB-infowindow CDB-infowindow--dark js-infowindow" style="background:#2E3C43">
  <div class="CDB-infowindow-close js-close"></div>
  <div class="CDB-infowindow-container">
    <div class="CDB-infowindow-bg">
      <div class="CDB-infowindow-inner js-inner">
        <ul class="CDB-infowindow-list js-content"></ul>
      </div>
    </div>
    <div class="CDB-hook">
      <div class="CDB-hook-inner"></div>
    </div>
  </div>
</div>
```

**Legend**
```
<ul>
  <li class="Legend-categoryListItem u-fex u-alignCenter">
    <span class="Legend-categoryCircle" style="opacity:1; background:#EE4D5A;"></span>
    <p class="Legend-categoryTitle CDB-Text CDB-Size-small uupperCase u-ellipsis" title=""></p>
  </li>
</ul>
```

To create the Widgets, click on the widget column. One widget will display the data as a
histogram, using the maroon color ramp. The other will display the data as a formula, using
the SUM operation on the column with your population data. Name the first widget population
explorer, and the second visible [population name.]

### 2C. Fire and State Data tabs

To create the state data tab, follow the same steps for importing the data outlined above for
the place-level data. There are no widgets associated with this data set. The CSS codes for
each of the style levels follows:

...
...
...
**TODO: finish copying over the readme**
...
...
...