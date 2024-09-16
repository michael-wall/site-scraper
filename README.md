**Introduction**

This module can be used to export the Private Pages of a Liferay Site to HTML. The module exposes a custom Gogo shell command: siteCrawler:crawlPages

This module has been tested in a local environment with JDK 8, Liferay DXP 7.4 U92 and OpenID SSO enabled.
The module has also been tested in a Liferay PaaS environment with JDK 11, a more recent Liferay DXP quarterly release but without OpenID SSO enabled.

**Usage**

The syntax and arguments to call Gogo shell command are as follows:

siteCrawler:crawlPages "20096" "34418" "mw.com" "http://mw.com:8080/group/intranet" "crawler@mw.com" "6a453159466e4f503477796746574c5a6a73756931413d3d" "456f74356e432b735a353771386c4444664a734e68773d3d" "/opt/liferay/tomcat/temp"

Note: All arguments are passed as String values with quotes and a space separator.

Arguments:

- companyId: The companyId of the Virtual Instance that the Site resides in.
- siteId: The siteId of the Site to be crawled.
- cookieHostName: The hostname used to access the Site e.g. mw.com
- layoutUrlPrefix: The base URL used when accessing the Site e.g. http://mw.com:8080/group/intranet
- emailAddress: The email address of the user to log in as. See 'Crawler User Account' section.
- emailAddressEnc: The encrypted email address of the user. See 'Crawler User Account' section.
- passwordEnc: The encrypted password of the user. See 'Crawler User Account' section.
- outputBaseFolder: The base folder that the output should be written to. A timestamp based folder will be created within this base folder e.g. siteExport_1726484407262

**Crawler User Account**

The module is designed to use a non-SSO enabled account to perform the crawling. In addition:

- The Instance Settings > User Authentication > 'Allow users to automatically log?' setting must be enabled while the tool is being setup and used. The setting can be disabled afterwards if not required. 
- The User used must be a non-SSO user and must have access to the Site and must have access to all the Pages that are to be exported.
- If necessary, create a Public page and add the 'Sign In' widget. This isn't necessary for the crawler to work but may be required to successfully login as the non-SSO user in a SSO enabled environment during setup. This page can be deleted once the encrypred credentials have been extracted. 
- To get the encrypted emailAddress and password values, perform a non-SSO login as the user in Chrome Incognito Mode with 'Remember Me' checked, then go to Dev Tools > Application > Storage > Cookies and copy the values of the ID and PASSWORD cookies.
- The ID cookie value from above should be passed as the emailAddressEnc argument.
- The PASSWORD cookie value from above should be passed as the passwordEnc argument.

**Copying the HTML files**
