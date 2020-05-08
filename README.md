# ML with Phishing

The files in this repo will be used for my "Machine Learning with Phishing" series on [my blog](https://andpalmier.github.io/posts/), please refer to the original blog post to have a more pleasant (dark mode included! 😈) reading experience.

Please, note that the small version of the dataset contains the 10 '*baseline features*' that were selected in [this study](https://www.sciencedirect.com/science/article/pii/S0020025519300763).


## Features

Here are the *baseline features* which were used in the posts.

|No. | Identifier 	 		      | Value type  | Description 																						    |
|:--:|:--------------------------------------:|:-----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 1  | **NumDash**    	  		      | Discrete    | Counts the number of "-" in webpage URL. 																		    |
| 2  | **NumNumericChars**    		      | Discrete    | Counts the number of numeric characters in the webpage URL. 																    |
| 3  | **NumSensitiveWords**  		      | Discrete 	| Counts the number of sensitive words (i.e., "secure", "account", "webscr", "login","ebayisapi", "signin", "banking", "confirm") in webpage URL. 					    |
| 4  | **PctExtHyperlinks**   		      | Continuous	| Counts the percentage of external hyperlinks in webpage HTML source code. 														    |
| 5  | **PctNullSelfRedirectHyperlinks**      | Continuous  | Counts the percentage of hyperlinks fields containing empty value, self-redirect value such as "#", the URL of current webpage, or some abnormal value such as "file://E:/". 		    |
| 6  | **FrequentDomainNameMismatch** 	      | Binary 	| Checks if the most frequent domain name in HTML source code does not match the webpage URL domain name. 										    |
| 7  | **SubmitInfoToEmail**		      | Binary 	| Check if HTML source code contains the HTML "mailto" function. 															    |
| 8  | **PctExtResourceUrlsRT**		      | Categorical | Counts the percentage of external resource URLs in webpage HTML source code. Apply rules and thresholds to generate value. 								    |
| 9  | **ExtMetaScriptLinkRT** 		      | Categorical | Counts percentage of meta, script and link tags containing external URL in the attributes. Apply rules and thresholds to generate value. 						    |
| 10 | **PctExtNullSelfRedirectHyperlinksRT** | Categorical | Counts the percentage of hyperlinks in HTML source code that uses different domain names, starts with "#", or using "JavaScript ::void(0)". Apply rules and thresholds to generate value. |

