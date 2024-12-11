---
Title: UnEssay
Project: Network Analysis of the ALIU Red Flag Names Report
Class: HIST5706
Student: Liran Assaf
---
## **Introduction**
I began my project by creating a brainstorming mind map of potential project pathways that I could pursue. I wanted to do something that would be beneficial to my thesis and thought of the different obstacles I’ve encountered since I started my research. A big challenge I've faced has been trying to translate a physical book from its original language to English. The trouble doesn’t just lie in the translation, but the extraction of text and conversion from physical to editable, digital content. We spoke extensively in class about OCR and on the different ways to pull text from documents, and ways to recognize and extract handwriting. Thus, my initial plan was to follow Andrew Akhlaghi’s OCR and Machine Translation tutorial and learn how to pull non-English text from a pdf and translated the writing to English. My hope was to use this to translate a crucial source for my thesis; a physical book that is entirely in Croatian.
___
![[xmind mindmap.png]]
___
## **OCR and Machine Translation**
In following this tutorial, my first mistake was trying to do everything in the command line as instructed. Unfortunately, the ImageMagic software required has been updated since the tutorial was written in 2021, and I encountered many errors and obstacles including the code syntax which has changed with the new ImageMagic version. It did not occur to me to take advantage of the virtual computer that Google Colab (GC) has to offer, and I installed a great number of things onto my hard drive while trying to follow the OCR tutorial that was promptly deleted after hours of hitting walls.

I changed my process, and moved to Google Colab to alleviate the burden on my computer. I encountered some issues in GC as well, and had to do some research on how to overcome the errors I was seeing. After altering the security policy for ImageMagic, I was able to follow the tutorial and successfully translate the given sample document from Russian to English via Tesseract.

The notebook was working and could successfully convert .pdfs to .tiff, and extract the text. However, the tutorial used Yandex to translate the converted .tiff documents, and I repeatedly ran into this error:
___
![[error message OCR notebook.png]]
___
I could not find any explanation or solution to this error, so rather than using Yandex, I altered the code slightly so that it would use Google Translate instead as it was already an available engine, and it worked quite well. The caveat was that Google Translate only allows for the translation of a limited amount of characters without an API, and realistically, this snippet of code/GC notebook wasn't sufficient for the amount of translating I would have needed to do to translate an entire book.

The extraction element of the notebook was quite handy, and I thought I would test it out on some pdfs that I had collected for my thesis with important information relating to my research. However, another problem that I encountered is that the OCR capabilities of ImageMagic are limited when it comes to reading the information from the target document when the formatting is different than a standard letter. The records that I had were horizontal in orientation, with data written in table format, which resulted in a very muddled, slop of words with unrecognizable characters.
___
![[OCR output AH records.png]]
___
I had previously typed this data out by hand:
___
![[AH records.xlsx.png]]
___
but I was hoping that this (cheat) code could help speed up the process when it came to extracting data from a record formatted as a table.


After hitting this wall, I moved on to a new idea for my project.

## **Open Refine**
The Art Looting Investigation Unit Red Flag Names report lists over one thousand individuals involved in art looting primarily during the Second World War. The report names the individual, their address and city of residence (if known), and a small blurb summarizing their suspicious/illicit activities that landed them on the watchlist. The original report is 175 pages long and is divided into countries where the people of interest primarily operated. I have seen many of these names in passing during my time researching for my thesis, and most importantly mentioned on the  Custody Receipts on Restitution to Yugoslavia from the Ardelia Hall Collection: Munich Administrative Records that list all the art that was released into the care of Ante Topic Mimara from the Munich Central Collecting Point in 1949.

Once I had established which database I wanted to use, I wanted to clean up the data in an easy to read way. Lootedart.com has all the information from the AILU record uploaded to the website: [Art Looting Intelligence Unit (ALIU) Reports 1945-1946 and ALIU Red Flag Names List and Index](https://www.lootedart.com/MVI3RM469661), but the information is formatted in a muddled way, if you wanted to see the different columns of information. 
In his tutorial [Fetching and Parsing Data from the Web with OpenRefine](https://programminghistorian.org/en/lessons/fetch-and-parse-data-with-openrefine), Evan Peter Williamson details how to organize data from a website in a readable way that is separated into neat columns. 
This is how the information is presented on the Looted Art website:
___
![[LootedArt report.png]]
___
I wanted to separate the information in these blocks into categories: name, location, content/information. At this point in time, my thinking was that if I separated out the information, it would be easier to read and then graph in Palladio according to the way the author of the [From Hermeneutics to Data to Networks: Data Extraction and Network Visualization of Historical Sources](https://programminghistorian.org/en/lessons/creating-network-diagrams-from-historical-sources) tutorial arranged his data. 

The Open Refine tutorial took Shakespeare's sonnets from one long document on the Project Gutenberg website and arranged them in such a way that each cell had an entire sonnet, followed by information about it in the next columns. 

The end goal of the tutorial wasn't necessarily what I wanted to achieve with my data, but there were elements of the tutorial that were applicable to my work. I played around with Open Refine quite a bit to get a better feel for it. 

The process to clean up the data from lootedart .com was not without its challenges, but I managed to get the data separated into different columns and cleared of any unnecessary HTML jargon:
___
![[ALIU Open Refine.png]]
____
The problem was, whereas I wanted name, location, and context/information, I could not work out a way to differentiate the information in "text clean 2" between 'location' and 'other information'. Regardless, I still had managed to separate the information and now had three distinct columns with different information. 
But I wanted to visualize the connections between the individuals on the list, and while Open Refine did a nice job of separating the block text, it was no better or different than what I could have done by hand. In fact, had I done this by hand, the names would have been formatted in a 'first name last name' way, and there would have been a distinction in the second column between location and context/information. I ultimately decided to move on from Open Refine and try something else that would have given me better, cleaner results. 

## **Data Extraction**
The next avenue I tried for my project was using the "structured-data-extractor-using-groq-and-llm-and-coreferee.ipynb" GC notebook to try and extract the relationships and connections of different people, institutions, and events from the ALIU report. 

I was beginning to feel frustrated with how the project was progressing because I kept hitting roadblocks and errors in the code I was using, but I did not have enough knowledge of Python to understand how to correct the issues or even what each line of code did to contribute to the larger goal of the notebooks I was creating/using.

In an effort to understand better and learn more about what I was doing, I took the "structured-data-extractor-using-groq-and-llm-and-coreferee.ipynb" GC notebook and spent quite a bit of time learning what each line did and commented out its function in a new notebook that I was creating as I was going along. Essentially, I had the original notebook open on one screen, and a new notebook open on another, and I went down each line, wrote it into the new notebook and added comments that explained me what each line did for current and future reference. This was important to me, because it gave me a base understanding of how the notebook ran and the process that resulted in the .csv output with the network connections based on the text it was given.
___
![[MASTERdata_extractor_SG_Copy with comments.png]]
___
I started off by using the notebook with the pre-loaded text about Giacomo Medici to gauge how it works, and to understand the connections that are picked out of the sample passage. Once I could understand, and read where the output information was coming from, I wanted to try the code on a sample text from my own research. I've been working on a timeline that I've compiled by pulling information from various sources about the central person and event my thesis focuses on. I initially thought that this would be a useful text to extract possible network connections from because it would help me to visualize a timespan of about 80 years in a way I hadn't yet been able to visualize. However, my timeline wasn't formatted in a way that was easy for the LLM to draw connections because as it stands, it is written in a way that makes sense to my brain and my way of thinking and not necessarily in an easily digestible way as there are abbreviations and references to things that the LLM didn't know about without the proper context. I felt that I was back at square one without any direction, but I was excited at the prospect of the code's capabilities. So rather than look at my own research, I decided to approach this in a different way and extract information from an established database that is connected to my work in such a way that will help my future research. 

I felt that extracting connections between the individuals on the Red Flag Names report and then generating a graph to better illustrate those connections would not only show the report in a new light, but could serve as a foundation for my own research as I would have a visual database for people of interest who might have/would have crossed paths with Ante Topic Mimara. I wanted this graph to be a starting point where I could potentially compare/overlay a graph of connections of a smaller scope and see if new connections are revealed. This project thus serves as a starting point for the *digihum* side of my thesis.

The report is organized in alphabetical order by last name, categorized by country (Germany, France, Switzerland, Netherlands, Belgium, Italy, Spain, Portugal, and Luxembourg). To first test the code, I took a small sample of 9 individuals and their respective snippets of information:
___
1. *Abb, Dr Gustav. Director of University Library, Berlin. 1940 appointed Director of Hauptverwaltung der Bibliotheken in Cracow. Reported responsible for looting of valuable treasures from Polish libraries.*
2. *Abels Brothers, Hermann. Cologne, Komoedienstrasse 26. Dealers. Specialists in 16th to 19th century painting and graphic arts. Active in Paris. In touch with Wuester, who was advised on purchases for Ribbentrop.*
3. *Abetz Otto. German Ambassador to France. Connected with the early seizures of Jewish art collections, particularly through the Kunsberg organisation.*
4. *Adriani Gert. Director of Kunsthistorisches Museum, Vienna. Contact of Miedl in Holland.*
5. *von Ahrendt, Bono. Director of Reichskammer fur Bildende Kunst. Active in Paris in 1942. In touch with Dr Epting.*
6. *Angerer, Josef (Sepp). Berchtesgaden. After Hofer, Goering’s most important buyer. Ardent Nazi, known to have had Gestapo connections. Member of firm of Quantmeyer & Eicke. Active throughout Europe, notably France and Italy. Contact of Reber, Ventura, Contini-Bonacossi, Ginori and Arturo Grassi. Was under temporary house arrest at Berchtesgaden, house of Fritz Goernnert, autumn 1945.*
7. *Apfelstaedt, Dr Hans Joachim. Dusseldorf. Karltor 1 - Cologne. Official purchasing agent for Dusseldorf and for Dusseldorf-Koln-Aachen-Bonn Gauleitung, for which he was active in France. Head of committee for research on cultural objects ‘looted ‘ from the Rhineland in previous wars. Assisted by Rademacher and Bammann.*
8. *Aubin, Dr Hermann Breslau 13, Kaiser Wilhelmstr 118. Professor of History at Breslau. Lectured in Poland 1940. One of the creators of Polish Volksdeutsch movement. Reported to have information concerning looted works of art in Cracow.*
9. *Augsburg, Dr. Berlin. Reported active in looting in Poland.**
___

To fit in the line of code, I formatted the paragraph by removing the paragraph spaces (^p) and replacing them with \n\n to indicate a new paragraph line in the original text. 

___
	*Abb, Dr Gustav. Director of University Library, Berlin. 1940 appointed Director of Hauptverwaltung der Bibliotheken in Cracow. Reported responsible for looting of valuable treasures from Polish libraries.\n\nAbels Brothers, Hermann. Cologne, Komoedienstrasse 26. Dealers. Specialists in 16th to 19th century painting and graphic arts. Active in Paris. In touch with Wuester, who was advised on purchases for Ribbentrop.\n\nAbetz Otto. German Ambassador to France. Connected with the early seizures of Jewish art collections, particularly through the Kunsberg organisation.\n\nAdriani Gert. Director of Kunsthistorisches Museum, Vienna. Contact of Miedl in Holland.\n\nvon Ahrendt, Bono. Director of Reichskammer fur Bildende Kunst. Active in Paris in 1942. In touch with Dr Epting.\n\nAngerer, Josef (Sepp). Berchtesgaden. After Hofer, Goering’s most important buyer. Ardent Nazi, known to have had Gestapo connections. Member of firm of Quantmeyer & Eicke. Active throughout Europe, notably France and Italy. Contact of Reber, Ventura, Contini-Bonacossi, Ginori and Arturo Grassi. Was under temporary house arrest at Berchtesgaden, house of Fritz Goernnert, autumn 1945.\n\nApfelstaedt, Dr Hans Joachim. Dusseldorf. Karltor 1 - Cologne. Official purchasing agent for Dusseldorf and for Dusseldorf-Koln-Aachen-Bonn Gauleitung, for which he was active in France. Head of committee for research on cultural objects ‘looted ‘ from the Rhineland in previous wars. Assisted by Rademacher and Bammann.\n\nAubin, Dr Hermann Breslau 13, Kaiser Wilhelmstr 118. Professor of History at Breslau. Lectured in Poland 1940. One of the creators of Polish Volksdeutsch movement. Reported to have information concerning looted works of art in Cracow.\n\nAugsburg, Dr. Berlin. Reported active in looting in Poland.\n\n*
___
After running this through the GC notebook, I was pleased to see the following results: 
___
![[Data Extractor first test ALIU.png]]
___
This result felt successful to me. There were additional columns and connections that could have been made by a human going in (which I will touch on later!), but the generated predicates were true to the text, and the output was clean and clear. 

The ALIU report lists over 1000 individuals and I felt that the scope was too large for the purpose of this project, so I decided to only look at the individuals from Germany. I worked methodically in small sections going by last name along the report and generated .csv files with network connections using the notebook. 
___
![[files of names in alphabetical order.png]]
___
Unfortunately, when I got to letters 'H' and 'G', I had maxed out my Google Colab GPU allowance, and it was asking for a paid subscription to proceed with using the GPU runtime type. This kind of threw a wrench in my plan because I had 18 more letters to get through in order to create a substantial graph. My problem too, was that working with a smaller size would be fine under other circumstances, but in this case, there are individuals with last names that begin with 'W' connected to individuals with last names that begin with 'A', but if I did not include the later individuals in the graph, no connections would be made. 

So I took matters into my own hands. 

Working based on the format of the generated .csv file, I went in and wrote all the connections by hand for each of the 492 individuals on the list under the 'Germany' category. 
___
![[ALIU source relationship target masterlist.png]]
___

## **Palladio**

My original intention was to use Palladio to graph my the ALIU networks. I followed Marten Düring's tutorial on how to use Palladio which felt useful and relevant to my work as his example taught readers how to graph Ralph Neumann's connections during the Second World War. I refreshed my memory and redid the tutorial using Düring's data to refamiliarize myself with Palladio. 
When I was ready to use my own data, I selected a small sample size from my master list and made two separate csv files (nodes and edges) in order to create a bipartite graph. 
___
![[nodes and edges for palladio.png]]
____
The resulting graph on Palladio was a good start to what I was hoping would eventually become a large-scale complex network graph. 
___
![[Palladio ALIU graph.png]]
___
I wanted to visualize the network in a more comprehensive way, and to be completely truthful, I do not really like Palladio's interface and the constantly moving graph does not work for me. 

## **Gephi**
I decided I wanted to try my hand at Gephi, and so once I was done my master list of German individuals from the ALIU report, I went in and cleaned up the graph and again created two different .csv files; nodes and edges. 

I began by importing both my nodes.csv and edges.csv files into Gephi. Gephi seems quite daunting at first, and I did not know how to proceed, so I found a tutorial on YouTube and followed the instructions.

What I like about Gephi versus Palladio, is that you can adjust the node size according to degree which makes the final graph easy to read as the larges nodes are the ones with the most traffic/connections. 

The ForceAtlas 2 is a directed graph that creates a kind of attraction and repulsion amongst the nodes to create a spongy circular network with numerous curved lines (edges) connecting the different nodes to one another. The main body of the graph is in the center, and the node pairings that surround the main body are the outliers or lesser-connected points. 

I like the ForceAtlas 2 graph in comparison to the Fruchterman Reingold layout for example, because the ForceAtlas 2 offers weighted edges and has the ability to prevent node overlap. The graph looked more natural and organic to me in comparison to the rigid circle of the Reingold graph. 

Under the statistics tab, I ran the average weighted degree report so that Gephi could determine the most influential nodes. From there, it was simply a matter of playing around and adjusting the scale and gravity, weight and colours of the graph before moving on to the preview tab of the graph which allowed me to adjust the final look of my network. 
___
![[Gephi ALIU graph overview page adjustments.png]]
___
My complete graph was neatly presented in such a way that illustrated the main 'popular' individuals from this section of the graph and was an amazing way to see the various network and social connections that existed between nearly 500 people. 
___
![[gephiGERMANNAMES.svg]]
___
![[close up of gephiGERMANNAMES graph.png]]
___
## **Gephi/Data Methodology**

It was a complex process to format the master list .csv files in a way that captured the information while remaining loyal to the context and integrity of the report. While writing out the connections, I erred on the side of caution and would prefer to create a potential repeat node than accidentally omit a connection. I also wanted to stay consistent with the predicates and tried to stick to a select number of them so that there was not any confusion. If there were repeat job titles for example, those became their own predicate (see "director of" "head of" "assistant to"), but the rest fell under "worked as" and the job title remained in the "Target" column if it was especially unique. 
These were the predicates used:

|                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| acquired<br>active as<br>active in<br>advisor to<br>agent for<br>alias<br>archivist for<br>arranged<br>assistant to<br>assisted<br>assisted by<br>assisted in<br>bought<br>business manager of<br>buyer for<br>buyer in<br>buyer of<br> | client of<br>collaborated with<br>commander of<br>Commissioner of<br>confiscated<br>connected to<br>connected with<br>conntected to<br>conntected to <br>consultant to<br>contact of<br>curator at<br>director of<br>dismissed from<br>editor of<br>exchanged<br>exported<br>fled to<br>founder of<br>friend of<br> | gave<br>had access to<br>has information about<br>hausmeister of<br>head of<br>implicated in<br>in charge of<br>in collaboration with<br>in contact with<br>in correspondence with<br>in custody<br>in custody at<br>in custody of<br>informer for<br>intermediary in<br>involved in<br>involved with<br>liason with<br>looted<br>member of<br>moved<br> | official of<br>operated by<br>opposed to<br>orchestrated<br>ordered<br>organized<br>owned<br>owner of<br>partner of<br>possessed<br>presented<br>protector of<br>purchased<br>purchased for<br>purchased from<br>purchased in<br>purchasing agent for<br>received<br>recipient of<br>related to<br>removed<br>replaced<br>represented<br>responsible for<br> | secretary of<br>sent<br>served in<br>shipped through<br>smuggled<br>sold to<br>stole<br>stored<br>succeeded<br>successor to<br>supplied agents with<br>took<br>took part in<br>tried to obtain<br>was<br>was an<br>worked as<br>worked at<br>worked for<br>worked in<br>worked with<br> |

Names are important because they are what establish the connections between the individuals. The original report often references someone in the information/context blurb of another figure by last name only: *"Bogner, Michael. Munich. Assistant to Bornheim."*
Once I had gone through the list in its entirety, I made sure that every name was spelled correctly and that first names were added to the last name mentions to ensure that the connections could be made. *"Michael Bogner	assistant to	Walter Bornheim"*

After the creation of the graph, I can go in and see that there are certainly tweaks to be made in the phrasing of some of the content under the "Target" column, and possibly too with the predicates. I also want to revisit the report and add the rest of the individuals from the other countries and include the location and address of the individuals that was provided and add that information to the .csv so that I could also graph geographical data. 

My goal is to use the data extractor notebook fully, or another model that can extract the necessary information from a chunk of written data. With the Google Colab limitations and obstacle I ran into with the request for payment and denied access to the GPU runtime type, I elected to type out the connections for the benefit of this project. While it was a lot of work to do, I feel that I developed an intimate relationship with the data and could understand the graph because I was familiar with the key figures and relationships in a way I might not have been had everything been done for me. There are pros and cons to both approaches, but I am glad I was able to experience both and see how they differ and can continue confidently from here. 

### **GRAPH COMPARISON**
The purpose of creating a network of the ALIU Red Flag Names report was to create a foundation for my future research because there are figures, institutions, events... that are mentioned in the original report that are connected with Ante Topic Mimara and his theft from the Munich Central Collecting Point. I wanted to see the which figures overlap with the MCCP report of the artworks released to Mimara in the hopes of drawing further connections between individuals involved in art crime and the works of art that Mimara ended up with. 

Ardelia Hall was an art historian and cultural affairs officer at the United States Department of State, who specialized in Nazi-looted art and assembled/reviewed many files connected with art theft and restitution claims post-war. On the reports that list the 166 works of art erroneously restituted to Mimara, Hall wrote in the margins additional information related to the pieces themselves. 
___
![[AH ATM report page 36.png]]
___
Here, in the margins of painting no. 18, she wrote *Bruschwiller aus deutschen besitz* which means "Bruschwiller from German ownership". From this, we can gather that this painting was in the possession of Eugen Bruschwiller who obtained it from a German individual. No. 19 says *Poussin v. Theo Hermssen Paris via Dorotheum*. We know then that this painting was connected to Theo Hermssen Jr., and was possibly in Paris at one point (Hermssen was from Paris), and it was connected to Dorotheum which was an important auction house in Austria. 

Hall added many notes to the margins of this particular file relating to Mimara. I took the works of art that she added additional information to and isolated just the paintings. 
___
![[AH paintings ATM from margin notes.png]]
___
First, I graphed just this dataset to see the connections between the different paintings before comparing them to the large ALIU data corpus. 
___
![[AH ATM record graph.png]]
___
Once I was able to visualize this smaller-scale data, I inserted the written information into the ALIU nodes and edges .csv files in order to create one large graph. But I needed to find a way to visually differentiate between the two datasets in order to see the new connections better. I added a new column called 'graph source' and sorted the two data sets between 'Graph A' and 'Graph B'. 

Once I had created the new graph and formatted it the way I wanted, I changed the colours of the nodes and edges according which data set they were from.
___
![[changing colours according to graph source.png]]
___
I was happy with this result as it was now easy to see how the new paintings were connected to the names from the ALIU report. Beyond that, I could see other possible connections by looking at the nodes from the original graph. 
___
![[GAHGRAPH.svg]]
___
![[close up of GAHGRAPH.png]]
___

### **CONCLUSION**
My progress throughout this project was not one without challenges; for a while I felt that I was hitting every roadblock imaginable and I was *erring* more that I was succeeding. But I don't regret my mistakes because I learned from each one and benefitted from having to find various work-arounds. 
I hope to continue this project as I develop my thesis because it has become an integral part of my understanding of not only the historical time period, but of the technological side of my work. I strengthened my understanding of Google Colab, Python, LLMs, graphing theory, graphing software and historical document visualization. I am going to continue with the ALIU list, and my goal is to create a graph with every entry from the report in order to create a comprehensive visualization of all the individuals involved in art crime during the Second World War. This will set up the foundation for my research of Mimara and will become an important corner in my thesis research. 