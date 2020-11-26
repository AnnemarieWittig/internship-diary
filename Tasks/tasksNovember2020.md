## past steps from 09.10.2020 week
* [x] Include a test-system, to figure out whether or not a file was fully translated and give a warning if it was not.
	* Any not-translated line is recognized by the value 'Enter your translation here'.
	* Additionally it might be necessary to test for empty strings in case a translator deleted the line.
	* The process should happen detached from the usual circle to not disrupt it.
* [x] Generate an access-key for the translation api.
* [x] Include the language negotiation in the code.

## Tasks done in November
* [x] Write a tool that accesses the translation-api and can automatically translate translation jsons
	* Machine genereated translations are tagged as {goallanguage]-t-{primelanguage}
	* If a translation starts in upper-case, whilst the original is no in upper-case, the entire line is transformed to lower-case
	* The subscription-key and location need to be given as a value
	* The service used is Azure Cognitive Translation Service
* [x] Expand the content negotiation proxy with according language negotiation
	* For the site-navigation there is now a prime-language to be set when starting the service. It defines the language of the basic structure of the URLs. Current possible structures are:
		* English: /doc/applicationprofile /doc/implementationmodel /doc/vocabulary
		* Dutch: /doc/applicatieprofiel /doc/implementatiemodel /doc/vocabularium
		* German: /doc/anwendungsprofil /doc/implementierungsmodell /doc/vokabular
	* The display-able pages however are chosen based on the prefered language of the browser _if_ any of the prefered browser language is listed in our list of accepted ones
	* If we get no accepted language, an error will occur
	* If a resource in a different language is wished for, the explicit path must be given
* [x] Create a multilingual subjectpage view
	* For the subjectpage, the labels are now displayed according to the browser's prefered language following the same rules as above
	* There is now the possibility to link the listed properties to a page describing their specification
	* The according variable is propLink and must be listed at all times in code, even if empty. It is treated similar as propLabel and propType and needs to be accessible for the template file
	* The different subjectpages are already translated but only the concept and conceptscheme are translated according to the official specification as the others have yet to be tested and aligned properly 
	* Current translations available are: English, Dutch
* [x] Adjusted the html-generator and templates
	* We have now neutral HTML templates. They still use the css files of Data-Vlandeeren though which causes the small logo to still appear in the tab-card in the browser
	* [Task from previous weeks] The wrongfully displayed titles are now fixed. The error occured due to the title being treated in both the data parser and the templates as a language-aware value whilst it was not in the actually created jsonld. 
	  It is now language neutral at all points in code. To specify a title according to its language it is set in the config file for each eap under "translation" in the respective language aware object
	* There is now an additional kind of template that allows a new column in the property list that points to external links. This template is found, for example, [here](https://github.com/Informatievlaanderen/duet/blob/master/templates/duet-ap2ext_en.j2)
	  and needs for each class and property a value called "externallink" - even if it is empty. This value is also language aware so it needs to be language-tagged. To create a template with this, the html-generator2.js needs to use the linkeddataparser4.js 
	  instead of the current (3rd) version of it as it needs to parse the additional value. It could also be adjusted so that the value does not _have_ to be present but to show the possibility and keep the code easily readable I did not do that.
* [x] Adjust the config for the jsonld generation in the first step of the flow to test and show the possibility of having a different prime language than Dutch
* [x] Inlcude a first small Demo of the entire flow
	* A fully written conclusion (what has been done, found and adjusted errors, remarks) on that can be found [here]()
* [ ] Include a demo with a full eap file