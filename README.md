# ML with Phishing

In this series of posts I am going to use [this dataset](https://data.mendeley.com/datasets/h3cgnj8hft/1/) to create a decision tree which (hopefully) will be able to identify a phishing website. Please, note that this dataset contains 48 features for every sample, which are **A LOT** for this task, indeed you can see that the [paper for which it was used](https://www.sciencedirect.com/science/article/pii/S0020025519300763) was about selecting the rigth features.

## Features

|No. | Identifier 	 		  | Value type  | Description 																						    |
|:--:|:----------------------------------:|:-----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 1  | NumDots    	  		  | Discrete    | Counts the number of dots in webpage URL. 																		    |
| 2  | Subdomain Level   		  | Discrete    | Counts the level of subdomain in webpage URL. 																	    |
| 3  | PathLevel  	  		  | Discrete    | Counts the depth of the path in webpage URL. 																		    |
| 4  | UrlLength  	  		  | Discrete    | Counts the total characters in the webpage URL. 																	    |
| 5  | NumDash    	  		  | Discrete    | Counts the number of "-" in webpage URL. 																		    |
| 6  | NumDashInHostname  		  | Discrete    | Counts the number of "-" in hostname part of webpage URL. 																    |
| 7  | AtSymbol 	  		  | Binary      | Checks if "@" symbol exist in webpage URL. 																		    |
| 8  | TildeSymbol 	  		  | Binary      | Checks if "∼" symbol exist in webpage URL. 																		    |
| 9  | NumUnderscore 	  		  | Discrete    | Counts the number of "\_"in webpage URL. 																		    |
| 10 | NumPercent 	  		  | Discrete    | Counts the number of "%" in webpage URL. 																		    |
| 11 | NumQueryComponents 		  | Discrete    | Counts the number of query parts in webpage URL. 																	    |
| 12 | NumAmpersand 	  		  | Discrete    | Counts the number of "&" in webpage URL. 																		    |
| 13 | NumHash 				  | Discrete    | Counts the number of "#" in webpage URL. 																		    |
| 14 | NumNumericChars    		  | Discrete    | Counts the number of numeric characters in the webpage URL. 																    |
| 15 | NoHttps            		  | Binary 	| Checks if HTTPS exist in webpage URL. 																		    |
| 16 | RandomString       		  | Binary 	| Checks if random strings exist in webpage URL. 																	    |
| 17 | IpAddress 	  		  | Binary 	| Checks if IP address is used in hostname part of webpage URL. 															    |
| 18 | DomainInSubdomains 		  | Binary 	| Checks if TLD or ccTLD is used as part of subdomain in webpage URL. 															    |
| 19 | DomainInPaths 	  		  | Binary 	| Checks if TLD or ccTLD is used in the path of webpage URL. 																    |
| 20 | HttpsInHostname 	  		  | Binary 	| Checks if HTTPS in obfuscated in hostname part of webpage URL. 															    |
| 21 | HostnameLength 	  		  | Discrete 	| Counts the total characters in hostname part of webpage URL. 																    |
| 22 | PathLength 	  		  | Discrete 	| Counts the total characters in path of webpage URL. 																	    |
| 23 | QueryLength 	  		  | Discrete 	| Counts the total characters in query part of webpage URL. 																    |
| 24 | DoubleSlashInPath  		  | Binary 	| Checks if "//" exist in the path of webpage URL. 																	    |
| 25 | NumSensitiveWords  		  | Discrete 	| Counts the number of sensitive words (i.e., "secure", "account", "webscr", "login","ebayisapi", "signin", "banking", "confirm") in webpage URL. 					    |
| 26 | EmbeddedBrandName  		  | Binary 	| Checks if brand name appears in subdomains and path of webpage URL. Brand name here is assumed as the most frequent domain name in the webpage HTML content. 				    |
| 27 | PctExtHyperlinks   		  | Continuous	| Counts the percentage of external hyperlinks in webpage HTML source code. 														    |
| 28 | PctExtResourceUrls 		  | Continuous 	| Counts the percentage of external resource URLs in webpage HTML source code. 														    |
| 29 | ExtFavicon 	  		  | Binary 	| Checks if the favicon is loaded from a domain name that is different from the webpage URL domain name. 										    |
| 30 | InsecureForms 	  		  | Binary 	| Checks if the form action attribute contains a URL without HTTPS protocol. 														    |
| 31 | RelativeFormAction 		  | Binary 	| Checks if the form action attribute contains a relative URL. 																    |
| 32 | ExtFormAction 	  		  | Binary 	| Checks if the form action attribute contains a URL from an external domain. 														    |
| 33 | AbnormalFormAction 		  | Categorical | Check if the form action attribute contains a "#", "about:blank", an empty string, or "javascript:true". 										    |
| 34 | PctNullSelfRedirectHyperlinks 	  | Continuous  | Counts the percentage of hyperlinks fields containing empty value, self-redirect value such as "#", the URL of current webpage, or some abnormal value such as "file://E:/". 		    |
| 35 | FrequentDomainNameMismatch 	  | Binary 	| Checks if the most frequent domain name in HTML source code does not match the webpage URL domain name. 										    |
| 36 | FakeLinkInStatusBar 		  | Binary 	| Checks if HTML source code contains JavaScript command onMouseOver to display a fake URL in the status bar. 										    |
| 37 | RightClickDisabled 		  | Binary 	| Checks if HTML source code contains JavaScript command to disable right click function. 												    |
| 38 | PopUpWindow 			  | Binary 	| Checks if HTML source code contains JavaScript command to launch pop-ups. 														    |
| 39 | SubmitInfoToEmail 		  | Binary 	| Check if HTML source code contains the HTML "mailto" function. 															    |
| 40 | IframeOrFrame 			  | Binary 	| Checks if iframe or frame is used in HTML source code. 																    |
| 41 | MissingTitle 			  | Binary 	| Checks if the title tag is empty in HTML source code. 																    |
| 42 | ImagesOnlyInForm 		  | Binary 	| Checks if the form scope in HTML source code contains no text at all but images only. 												    |
| 43 | SubdomainLevelRT 		  | Categorical | Counts the number of dots in hostname part of webpage URL. Apply rules and thresholds to generate value. 										    |
| 44 | UrlLengthRT 			  | Categorical | Counts the total characters in the webpage URL. Apply rules and thresholds to generate value. |
| 45 | PctExtResourceUrlsRT 		  | Categorical | Counts the percentage of external resource URLs in webpage HTML source code. Apply rules and thresholds to generate value. 								    |
| 46 | AbnormalExtFormActionR 		  | Categorical | Check if the form action attribute contains a foreign domain, "about:blank" or an empty string. Apply rules to generate value. 							    |
| 47 | ExtMetaScriptLinkRT 		  | Categorical | Counts percentage of meta, script and link tags containing external URL in the attributes. Apply rules and thresholds to generate value. 						    |
| 48 | PctExtNullSelfRedirectHyperlinksRT | Categorical | Counts the percentage of hyperlinks in HTML source code that uses different domain names, starts with "#", or using "JavaScript ::void(0)". Apply rules and thresholds to generate value. |

