# CRIMES-3
CRIMENES TIPO 3
Crime Data Explorer
Build status on CircleCI Code Climate GPA Dependency Status

This project is the front end for the Crime Data Explorer, using data from fbi-cde/crime-data-api. The Crime Data Explorer is a website that allows law enforcement and the general public to more easily access Uniform Crime Reporting (UCR) data. Over 18,000 city, university and college, county, state, tribal, and federal law enforcement agencies voluntarily report crime data to the program, and the FBI publishes it in annual reports.

Using the API Directly
API Base URL: https://api.usa.gov/crime/fbi/sapi

Requests Format: https://api.usa.gov/crime/fbi/sapi/{desired_endpiont}?api_key=<API_KEY>

See more information about API endpoints at https://crime-data-explorer-master.fr.cloud.gov/api API Requests are required to have an API Key appended to the request to sign up for an API key please vist https://api.data.gov/signup/

Example Requests:

https://api.usa.gov/crime/fbi/sapi/api/participation/national?api_key=XXX
https://api.usa.gov/crime/fbi/sapi/api/agencies?api_key=iiHnOKfno2Mgkt5AynpvPpUQTEyxE77jo1RU8PIv
Installation
You will need node and npm to install and run this project.

git clone git@github.com:fbi-cde/crime-data-frontend.git cde && cd cde
npm install
Running the app locally
The application expects a few environment variables to interact with the API:

CDE_API - this should be the URL for the API. To use the public API, set this to https://api.usa.gov/crime/fbi/sapi
API_KEY - this should match the key used by the API. If you are using the public API, sign up for an API key at https://api.data.gov/signup/
You can copy the env.sample file (cp env.sample .env), fill in your own values, and then make sure to source .env before running the build process.

Use npm run watch to start the continuous webpack processes and a webserver.

Running tests
You can lint the code with npm run lint and run tests with npm run test.

Running Selenium tests
Launch Selenium Stand-alone server with npm run selenium:start or npm run selenium:start:mac on a Mac. You will want to start this in a different shell or as a background task.
Ensure CDE is running locally
Configure test/browser/release_verification.js to use the port you have CDE running on
Execute npm run selenium:run - This will execute the automated test that covers the manual verification process
Updating agency data
We load a JSON file, sourced from the API, into the application that has all the agency ORIs and names to make the end user experience better. When we need to update that JSON file with new data from the API, we can just run npm run agencies and the data will be downloaded and gzipped properly. This is useful when agency names are updated.

Deployment
master branch
This project is continuously deployed to cloud.gov with every commit to the master branch. Right now, you can use the application at https://crime-data-explorer-master.fr.cloud.gov.

Stable
Tagged releases are deployed to https://crime-data-explorer.fr.cloud.gov.

Staging
A third, and less formal, environment is available at https://crime-data-explorer-staging.fr.cloud.gov. This is for ad-hoc usage and testing.

Use cf push -f manifest/staging.yml to deploy. Remember that cf pushes from your local file structure and won't build the app on its own, so make sure you run npm run build before pushing.

Release process
This app follows semver and has tagged releases by version number. You can see all notable changes in CHANGELOG.md.

We use the following criteria to determine the proper next version number. A major version change is appropriate when the URL structure has changed (breaking any existing URLs) or when there is a major removal of content. A minor version change is appropriate when the changes include more than bug fixes but not breaking changes. A patch version is appropriate when only bugs or security issues are addressed.

Manual verification
Though unit test coverage is decent (check with npm run coverage, as of cdb2340 it was about 77% of all statements), we run through a few basic user scenarios before tagging a release to check the application. We are working on getting the automated browser tests to replicate this exact process.

Load homepage from master branch. Can be local or https://crime-data-explorer-master.fr.cloud.gov
Select "Explorer" from navigation
Ensure that a trend chart renders to show "Violent Crime rate in United States"
Select "Alabama" as the location in the left hand side menu
Select "Robbery" as the crime in the left hand side menu
Ensure that the URL is now /explorer/state/alabama/robbery
Ensure that a trend chart renders to show "Robbery rate in Alabama, 2004–2014"
Scroll down and ensure donut charts, histograms, and tables render to show "Robbery incident details in Alabama, 2004–2014"
Scroll down and ensure there is a section called "About the data"
Select "Downloads & Documentation" from the navigation at the top of the page or the footer at the bottom
Select "Alabama" as the "Location" and "2000" as the "Year". Click download and ensure that a .zip file is downloaded
Click the "Download CSV" link in the "Hate Crime" dataset section under the heading "Additional Datasets" and ensure a file called hate_crime.csv is downloaded
Tagging a release
Compile the notable changes into the CHANGELOG.md. You can use the /compare/:lastVersion...master endpoint on Github. For example, this /compare link was used to determine the changes in v1.1.0
Determine if the version should be increased by a major, minor, or patch version
Adjust the version number in package.json accordingly
Submit a pull request without tagging the commit
Once the pull request is merged, tag the merge commit (on master) as vX.Y.Z where X, Y, and Z reflect the same version number as the now merged change for package.json
Push the tag to Github with git push origin vX.Y.Z
Browser support
We explicitly support Chrome, Safari, IE 10+, Firefox, and MS Edge.
