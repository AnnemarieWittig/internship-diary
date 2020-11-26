# Conclusion

For a first test-run of the workflow, an (incomplete) English eap file was created based on SDG-Sandbox educational evidence specification. The goal was to specify English as a prime and German as a targetlanguage. To start the test, the following steps had to be taken:
## Workflow
#### Setting up the work-environment
 1. A new workspace-repository was created based on the [OSLO-template](https://github.com/Informatievlaanderen/OSLOthema-template). The corresponding repository can be found [here](https://github.com/AnnemarieWittig/englishworkspace). Since this goes in a multilingual context, a translation directory had to be added into it.
 2. The [EAP-File](https://github.com/AnnemarieWittig/englishworkspace/blob/main/sdgmodels2.eap) was stored in the root-folder of that repository. 
 3. A configuration for that eap has been created. In our case I used four different ones to display the different document types (ap, voc, impl-ap and impl-voc). They were stored in the [config-directory](https://github.com/AnnemarieWittig/englishworkspace/tree/main/config). Each of them follows a similar structure but must have their respective information adjusted.
 4. For each config a base template that extends the duet templates had to be created and added into the [template-directory](https://github.com/AnnemarieWittig/englishworkspace/tree/main/templates).
 #### Adjusting the duet-repository
 5. With the workspace preparations concluded, the duet repository had to be configured accordingly. For all the new configurations, an English publication point had to be added into the [publication-json](https://github.com/Informatievlaanderen/duet/blob/master/config/publication.json) whilst the older ones had to be disabled due to the new prime language.
 6. The general configurations for the three document types [ap](https://github.com/Informatievlaanderen/duet/blob/master/config/config-ap.json), [voc](https://github.com/Informatievlaanderen/duet/blob/master/config/config-voc.json) and [oj](https://github.com/Informatievlaanderen/duet/blob/master/config/config-oj.json) had to be transferred to English, meaning that all the lang-values were set to en and the names adjusted accordingly.
 7. Shell scripts that create language aware files had to be adjusted. That means that for the [render-details.sh](https://github.com/Informatievlaanderen/duet/blob/master/scripts/render-details.sh) and for the [generate-voc.sh](https://github.com/Informatievlaanderen/duet/blob/master/scripts/generate-voc.sh) the prime and goal language was changed.
 8. Since this was the first time using German files, general German templates had to be created and stored in the [duet-templates](https://github.com/Informatievlaanderen/duet/tree/master/templates).
### The Actual Process
 9. Once all the changes are pushed and the circleci flow finished, the results are pushed into the [duet-generated-repository](https://github.com/Informatievlaanderen/duet-generated). Here one could jump into the editor role to test the whole process of translating. 
 10. The circle-ci already showed in the validate-and-generate-translation-report-step that it failed, meaning the translationfiles are not yet fully translated.
 11. The translation file is found in the report repository, directing oneself through the structure defined by the publication points, one of those files could be [this one](https://github.com/Informatievlaanderen/duet-generated/blob/master/report/doc/applicationprofile/sdg-ap/translation/sdgmodels2-ap_de.json). It must be remarked, that at the time this file had placeholders such as "Enter your translation here" which are not there anymore due to me finishing the translation process. For the sake of explaining, imagine it not to be finished.   
This file I then copied out and first translated it with the machine translation tool (remarks on that follow below) and by hand to have a well usable comparison.
12. The finished translated files had then to be wired back to the workflow by stashing them in the workspace's [translation-repository](https://github.com/AnnemarieWittig/englishworkspace/tree/main/translation) without changing their names.
13. A restart of the flow then updated all created files with the new translated values. 

## Remarks
It has to be pointed out, that once the "actual process" was reached, an iterative process of finding bugs, fixing them, testing again, finding the next ones, ... began. It did not go as smoothly as it is described above. However if you would replay this case, for you it should all work now.
### Errors found (and corrected)
In the whole process multiple errors occured. I will simply list them here and describe any solutions if they were special updates to the flow:

 - The first errors were all found with the translation-json. For some reason the attributes name and description were always tagged in nl (already in the jsonld) causing issues in the translations. Whilst the name probably is due to an error in the eap, the description was not. We decided to actually take the description out completely and instead use definition as both of these describe the same thing and the description was redundant already before.
 -  Since the name of an entity is language aware and treated as such but should not actually be translated, it is now added into the translation-json without a "Enter your translation here" placeholder but simply copied from the main to the goal language. 
 - Taking out the description caused another row of adjustments to some js tools as they accessed it. They now all use definition, rendering the description value obsolete and ready to be taken out at a later point in time.
 - The translation json will now display empty attributes, if they are not undefined in the jsonld, as empty objects in itself, too, to hint an editor that they might have forgotten some specification in their eap file
 - Whilst comparing files I realized that for voc-type specifications the baseURI is only listed within "extra" and not in the "root" of the json. This might be kept in mind for future adjustments.
 - When merging the translation json back into the jsonld there was an error in the bash script so that the wrong files were given to the js tool.
 - When adjusting the SHACL-generator regarding the description-definition changes another issue was discovered as to the treatment of empty objects. They used to appear as "'something': null". Now, empty attributes (names or description) are not displayed at all to ensure a clean ttl version.
 - Lastly for the ttl-files, the created uris usually end with a doubled language tag (enen) which is most likely due to the change of adding the language tags into all the files directly. This should be fixable by simply adjusting the config.

### Machine translations
So overall, even if that's just a very small scaled test, I'd say I am very impressed and did even go back to change some of my translations a bit (mainly due to me being very used to some English words I simply accepted or similar-in-meaning-words where I just thought theirs sounds better).  
The overall sentence construction and vocabulary was surprisingly really good and it didn't even translate proper names (INSPIRE Address Representation) which I definitely anticipated.  
The only difference I really see is for one translation, the "admin unit" I personally would have chosen a different translation in the context of the given definition (which bing didn't know) but then again the question is if one would really want that and that as a human I'd ignore things like "\t " if I feel like they don't belong (and as an editor would go back to the uml and adjust that) which a machine obviously does not do but here again is the question if that's really an issue considering it might even be of purpose that the formatting is kept.  
At this point I'd say the only real difference is that I chose some different sentence constructions here and there but the machine one's are grammatically completely correct so that's just up to personal preference

