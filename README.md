# SDK Test
Ext JS Sencha Test unit tests.

## Test Builds

### Full Test Builds

* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTestTeamcityMacNpm&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTestTeamcityMacNpm)/statusIcon"/></a> - Teamcity - Mac
* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTestTeamcityLinuxNpm&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTestTeamcityLinuxNpm)/statusIcon"/></a> - Teamcity - Linux
* [![Build Status](https://travis-ci.com/sencha/SDK-Test.svg?token=KdcJCzakCyZqGAcQgvVY&branch=7.0.x)](https://travis-ci.com/sencha/SDK-Test) - TravisCI - Linux

### Separate Test Builds

* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTests_SdkTestsDivided_SdkTestAdminDashboard&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTests_SdkTestsDivided_SdkTestAdminDashboard)/statusIcon"/></a> - Admin Dashboard
* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTests_SdkTestCalendar&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTests_SdkTestCalendar)/statusIcon"/></a> - Calendar
* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTests_SdkTestDesktop&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTests_SdkTestDesktop)/statusIcon"/></a> - Desktop
* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTests_SdkTestsDivided_SdkTestKitchenSinkRegress&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTests_SdkTestsDivided_SdkTestKitchenSinkRegress)/statusIcon"/></a> - Kitchen Sink Regression
* <a href="https://teamcity.sencha.com/viewType.html?buildTypeId=Orion_23_Test_EndToEndTesting_SdkTests_SdkTestsDivided_SdkTestKitchenSinkSmoke&guest=1"><img src="https://teamcity.sencha.com/app/rest/builds/buildType:(id:Orion_23_Test_EndToEndTesting_SdkTests_SdkTestsDivided_SdkTestKitchenSinkSmoke)/statusIcon"/></a> - Kitchen Sink Smoke

## Debugging
Load the [./senchaTest](/senchaTest/) folder into Sencha Test. 

## Building
See [./senchaTest](/senchaTest/) README.md.

## Development

### Running
The test suites run against the examples on staging. 

1. Fork project master branch
2. Open [./senchaTest] in Sencha Test
3. Select test suite and browser farm and run test.

### Target Goals

Automated tests have to run reliably on all P1 platforms, mainly Chrome, IE11, Edge, FF, Safari 10,9, Android 5,6 tablet and phones, iOS 9,10 tablets and phones. Other platforms are nice to have, tests should be runnable, but there is no need to fix all random failures.

### Development Goals

Add comment to file header about tested platforms When fixing tests we have clear idea which platforms worked or didn't work previously

Divide tests into **well-named** describes – it helps to narrow down reproducible test case and find root cause of failures. Describes are used to group together several related specs (it). Specs should be atomic and verify single feature/functionality.
Example : 
```javascript
describe('demo example') { 
    describe('grid panel 1'){ 
        describe('header'){ 
            it('title should contain some text') {
                expect(panel.getTitle()).toBe('title');
            }
            it('heder should docked to left'){
            } 
        } 
        describe('toolbar'){            
        } 
        describe('grid'){ 
            describe('header'){ 
            } 
            describe('body'){ 
            } 
        } 
    } 
} 
```
**afterAll/afterEach** - ensure that following tests are not affected when one spec block fails – for example you need to open some window and during test execution test fails, test needs to close that window in afterEach/afterAll section 
 
**ExtJS query locators** - we should rely mostly on ExtJs component selectors and not on HTML selectors (xpath, dynamic Id's). That's because HTML can easily change during the time, so information based on HTML structure are not reliable. 
 
**Prefix** - In KitchenSink each example should have custom **xtype** – use this as prefix for other query locators – this will ensure that you are selecting components within desired example and it should avoid interfering with other examples.  
 
**Shared library** - Factorize functions only if it's used by more tests, if you create function that is used by single test you should keep in the test file only, same applies if you need to use/generate some test data. 
Function that are added to CommonLib must be well documented so it's easy to understand what parameters should be passed, add funtions to appropriate scope – Lib, Lib.d3 ... 

### Formatting guidelines
We are following Sencha's code guidelines and general javsascript code style - http://javascript.crockford.com/code.html.

* Use 4 spaces to indent new line (not TAB) 
* camelCase variable naming 
* Capitalized variables should be reserved for PageObjects(SenchaTest) or Global variables 
* Use semicolon - ; at the end of statement 
* Avoid using global variables 
* Don't use white spaces in file/folder names 
* No commented code unless it's TODO 
* Use comments to explain complex/unique piece of code

