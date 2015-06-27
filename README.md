<html>

<head>
<meta http-equiv=Content-Type content="text/html; charset=windows-1252">
<meta name=Generator content="Microsoft Word 14 (filtered)">
<style>
<!--
 /* Font Definitions */
 @font-face
	{font-family:Calibri;
	panose-1:2 15 5 2 2 2 4 3 2 4;}
 /* Style Definitions */
 p.MsoNormal, li.MsoNormal, div.MsoNormal
	{margin-top:0in;
	margin-right:0in;
	margin-bottom:10.0pt;
	margin-left:0in;
	line-height:115%;
	font-size:11.0pt;
	font-family:"Calibri","sans-serif";}
p.MsoListParagraph, li.MsoListParagraph, div.MsoListParagraph
	{margin-top:0in;
	margin-right:0in;
	margin-bottom:10.0pt;
	margin-left:.5in;
	line-height:115%;
	font-size:11.0pt;
	font-family:"Calibri","sans-serif";}
p.MsoListParagraphCxSpFirst, li.MsoListParagraphCxSpFirst, div.MsoListParagraphCxSpFirst
	{margin-top:0in;
	margin-right:0in;
	margin-bottom:0in;
	margin-left:.5in;
	margin-bottom:.0001pt;
	line-height:115%;
	font-size:11.0pt;
	font-family:"Calibri","sans-serif";}
p.MsoListParagraphCxSpMiddle, li.MsoListParagraphCxSpMiddle, div.MsoListParagraphCxSpMiddle
	{margin-top:0in;
	margin-right:0in;
	margin-bottom:0in;
	margin-left:.5in;
	margin-bottom:.0001pt;
	line-height:115%;
	font-size:11.0pt;
	font-family:"Calibri","sans-serif";}
p.MsoListParagraphCxSpLast, li.MsoListParagraphCxSpLast, div.MsoListParagraphCxSpLast
	{margin-top:0in;
	margin-right:0in;
	margin-bottom:10.0pt;
	margin-left:.5in;
	line-height:115%;
	font-size:11.0pt;
	font-family:"Calibri","sans-serif";}
.MsoChpDefault
	{font-family:"Calibri","sans-serif";}
.MsoPapDefault
	{margin-bottom:10.0pt;
	line-height:115%;}
@page WordSection1
	{size:8.5in 11.0in;
	margin:1.0in 1.0in 1.0in 1.0in;}
div.WordSection1
	{page:WordSection1;}
 /* List Definitions */
 ol
	{margin-bottom:0in;}
ul
	{margin-bottom:0in;}
-->
</style>

</head>

<body lang=EN-US>

<div class=WordSection1>

<p class=MsoNormal>Genome Finder</p>

<p class=MsoNormal><u>Introduction</u></p>

<p class=MsoNormal>Genome Finder is a pipeline to conduct a <i>metabolic
inference</i> on a collection of 16S rRNA gene sequences.  Given a set of 16S
rRNA gene sequences the pipeline returns a collection of metabolic pathways
that are expected.  Genome Finder as designed with the analysis of large 16S
rRNA gene sequence libraries in mind, such as those generated by 454 or
Illumina sequencing, but is also appropriate for small datasets.</p>

<p class=MsoNormal><u>Requirements</u></p>

<p class=MsoNormal>Genome Finder requires a Linux-like operating environment. 
It was developed on Ubuntu.  Genome Finder uses several open source tools in
addition to some novel components.  Required tools that should be located in
your path are:</p>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in'>1.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span> Python
2.7</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>2.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Biopython</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>3.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>The
Python joblib module</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>4.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Blast+
(and the 16SMicrobial database)</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>5.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Mothur
(and one of the Mothur formatted alignment databases)</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>6.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>FastTreeMP</p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in'>7.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>pplacer,
Guppy, and taxit from the Matsen group</p>

<p class=MsoNormal><u>Components</u></p>

<p class=MsoNormal>Eight Python scripts are provided to create the database and
execute the metabolic inference.  The genome_finder.sh script is a template to
guide database construction and analysis.  An addition text file,
mean_phi_values.txt, creates some data on the available completed genomes that
is essential to Genome Finder.</p>

<p class=MsoNormal><u>Basic operation</u></p>

<p class=MsoNormal>The first time genome_finder.sh executes it must construct the
database necessary to conduct the metabolic inference.  Counterintuitively it
needs to run part of an analysis to construct the database.  Database
construction is very time intensive and can take several days, however,
subsequent executions are fairly fast.</p>

<p class=MsoNormal>Each script has, near the top, a set of variables that should
be modified by the user to reflect directory pathways and other aspects of the
operating environment.</p>

<p class=MsoNormalCxSpLast><i>genome_finder_make_ref.py</i> (only necessary to
construct database)</p>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in'>1.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span> Downloads
all completed genomes from Genbank</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>2.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Finds
the 16S rRNA genes in these genomes</p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in'>3.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Compiles
16S rRNA gene copy number with the provided phi values</p>

<p class=MsoNormal>genome_finder_place_it.py (necessary to construct database
and for analysis)</p>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in'>1.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span> Uses
the 16S rRNA genes from the completed genomes to build a reference tree with
FastTreeMP after alignment with Mothur</p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in'>2.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Uses
taxit to convert the alignment and tree into a reference package</p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in'>3.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Executes
pplacer to place query reads on the reference tree</p>

<p class=MsoNormal>genome_finder_build_core_genomes.py (necessary to construct
database)</p>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in'>1.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span> Uses
the reference tree and blastn to build a consensus genome for each node on the
reference tree.</p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in'>2.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Generates
statistics for each consensus genome, including size, expected degree of
genomic plasticity, and expected 16S rRNA gene copy number</p>

<p class=MsoNormal>*** IN PROGRESS ***</p>

</div>

</body>

</html>
