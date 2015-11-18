# nameworld
<html>
<head>
	<title> dream names </title>
<style>
#header {
    background-color:BLACK;
    color:white;
    text-align:center;
    padding:5px;
}
#PART1 {
    background-color:LIGHTGREEN;
    color:PURPLE;
    text-align:center;
    padding:5px;
}
#footer {
    background-color:BLACK;
    color:GREY;
    clear:both;
    text-align:center;
   padding:5px;	 	 
}
</style>

</head>
<body STYLE="BACKGROUND-COLOR:DARKGREEN";>
<CENTER>
<div id="header">
<h1 font="times new roman" color="blue">... DREAM NAME WORLD ...</H1>
</DIV>
</CENTER>
<br>
<br>


<br>
<br>
<CENTER>
<div id="PART1">

<H3><P STYLE ="TEXT-ALIGN:CENTER" STYLE="FONT-SIZE:600%">FIND NAMES RANKING IN YEAR...</P></H3>


<!-----FINDING THE TOP VALUES IN A PARTICULAR YEAR----->


<form action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>" method="post">

Year: <input type="text" id="year" name="year" required>
List: <select id="top" name="top">
		<option value="10">Top 10 </option>
		<option value="20">Top 20 </option>
		<option value="100">Top 100 </option>
		<option value="1000">Top 1000 </option></select>
Gender: <select id="gen" name="gen">
		<option value="male">Male</option>
		<option value="female">Female</option>
		<option value="both">Both</option>
		</select>	
		<input type="submit" value="Submit" name="submit">
		<br />
</form>

<?php
#----DISPLAYING LIST IN THE FORM OF TABLE----
$row = 1;
	if(isset($_POST['submit'])) 
	{
		echo"<center>";
		echo "<table border=1 cellspacing=0 cellpading=10 columnwidth=20>";
		echo "<tr><th>NAME</th>";
		echo "<th>AMOUNT</th>";
		echo "<th>RANK</th></tr> ";
	
		$gender=$_POST['gen'];
		$top=$_POST['top'];
		if($gender=="female"||$gender=="male")
		{
		$i=0;
		$file=$gender."_cy".$_POST['year']."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) 
		{
			fgetcsv($handle, 1000, ",");
			while (($data = fgetcsv($handle, 1000, ",")) !== FALSE && $i<$top) 
			{
				$i++;
        			$num = count($data);
        			$row++;
	 

        			for ($c=0; $c < 1; $c++) 
				{
            				echo " <tr> <td> $data[$c]</td>";
        `			}

				for ($c=1; $c < 2; $c++) 
				{
            				echo "<td> $data[$c] </td>";
				}
	
				for ($c=2; $c < 3; $c++) 
				{
            				echo "<td> $data[$c] </td></tr>";
        			}
	

    			}
		echo"</table>";
    		fclose($handle);
		}
		}
		else
		{
		$i=0;
		$file="female_cy".$_POST['year']."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) 
		{
			fgetcsv($handle, 1000, ",");
			while (($data = fgetcsv($handle, 1000, ",")) !== FALSE && $i<$top) {
			$i++;
        		$num = count($data);
        		$row++;
        		for ($c=0; $c < 1; $c++) 
			{
            			echo " <tr> <td> $data[$c]</td>";
        		}
			for ($c=1; $c < 2; $c++) 
			{
           			echo "<td> $data[$c] </td>";
			}
	
			for ($c=2; $c < 3; $c++) 
			{
            			echo "<td> $data[$c] </td></tr>";
        		}
	
    		}
   		fclose($handle);
		echo"</TABLE>";
		echo"&nbsp;&nbsp;&nbsp;&nbsp;FEMALES <br />\n";
		}
		$i=0;
		echo "<table border=1 cellspacing=0 cellpading=10 columnwidth=20>";
		echo"<br />\n<br />\n";
		echo "<tr><th>NAME</th>";
		echo "<th>AMOUNT</th>";
		echo "<th>RANK</th></tr> ";
	
		$file="male_cy".$_POST['year']."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) 
		{
			fgetcsv($handle, 1000, ",");
			while (($data = fgetcsv($handle, 1000, ",")) !== FALSE && $i<$top) 
			{
				$i++;
        			$num = count($data);
        			$row++;
        			for ($c=0; $c < 1; $c++) 
				{
             				echo " <tr> <td> $data[$c]</td>";
        			}
				for ($c=1; $c < 2; $c++) 
				{
            				echo "<td> $data[$c] </td>";
				}
	
				for ($c=2; $c < 3; $c++) 
				{
            				echo "<td> $data[$c] </td></tr>";
       				}
	
    			}
			echo"</table>";
			fclose($handle);
			echo"</TABLE>";
			echo"&nbsp;&nbsp;&nbsp;&nbsp;MALES <br />\n";
		}
		}
		
	}
?>
<br>
<br>

</DIV>
</CENTER>
<BR>
<BR>

<CENTER>
<div id="PART1">


<br>
<br>

<H3><P STYLE ="TEXT-ALIGN:CENTER" STYLE="FONT-SIZE:600%">CHECK POPULARITY CHANGE IN THE NAME...</P></H3>


<!-----SHOWING VARIATIONS IN CHANGE OF NAME FROM GIVEN YEAR TO LAST YEAR----->


<form action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>" method="post">
Name: <input type="text" name="name" required/>
Year: <input type="text" name="year" required/>
Gender: <select id="gen" name="gen">
		<option value="male">Male</option>
		<option value="female">Female</option>
		</select>	
<input type="submit" value="Submit" name="Submit">
</form>

<?php
#----RETRIEVING DATA FROM EACH REQUIRED FILE----

if(isset($_POST['Submit'])) 
{	$yes=1;
	$name=$_POST['name'];
	$gender=$_POST['gen'];
	$year=$_POST['year'];
	$plotdata=array(array('0000','sds'));
	$values=array();
	$data;
	$total=0;
	while($year<2014)
	{
		$file=$gender."_cy".$year."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) 
		{
			fgetcsv($handle);
			$count=0;
			while(($data = fgetcsv($handle)) !== FALSE ) 
			{
				if(((strcmp($name,$data[0]))==0)||((strstr($data[0],$name))!== FALSE))
				{
					if($count==0)
					{
						$values[$year]=$data[1];
						$count++;
					}
					else
						$values[$year]+=$data[1];
					#print_r($data);
					$total++;
					$yes=0;
					}
			}

		}
		$year++;
   		fclose($handle);
	} 
	if($yes)
	echo "No Record Found!!!";
	else
	{
	# ------- PLOTTING GRAPH FROM THE ASSOCIATED ARRAY ------
	if($total<15)
		$im_wdth=300;
	else if($total<60)
			$im_wdth=600;
		else
			$im_wdth=1300;
	$im_ht=400; 
	$mrgn=20;


	#-----FINDING GRAPH SIZE FROM IMAGE SIZE-----
	$gr_wdth=$im_wdth - $mrgn * 2;
	$gr_ht=$im_ht - $mrgn * 2; 
	$img=imagecreate($im_wdth,$im_ht);


	$bar_wth=10;
	$bar_numbr=count($values);
	$gap= ($gr_wdth- $bar_numbr * $bar_wth ) / ($bar_numbr +1);


	#-----ALOTTING COLORS TO DIFFERENT COMPONENTS OF THE GRAPHS-----
	$color_bar=imagecolorallocate($img,220,220,220);
	$bckgrnd_clr=imagecolorallocate($img,300,100,50);
	$brdr_clr=imagecolorallocate($img,0,0,0);
	$line_clr=imagecolorallocate($img,300,300,300);

	# ------FOR MAKING BORDER------

	imagefilledrectangle($img,1,1,$im_wdth-2,$im_ht-2,$brdr_clr);
	imagefilledrectangle($img,$mrgn,$mrgn,$im_wdth-1-$mrgn,$im_ht-1-$mrgn,$bckgrnd_clr);


	# -------FINDING SCALE THROUGH MAXIMUM VALUE-------
	$maxval=max($values);
	$ratio= $gr_ht/$maxval;


	# --------MARKING SCALE AND HORIZONTAL LINES IN GRAPH--------
	$lines=20;
	$horizontal_gap=$gr_ht/$lines;

	for($i=1;$i<=$lines;$i++)
	{
   		$y=$im_ht - $mrgn - $horizontal_gap * $i ;
    		imageline($img,$mrgn,$y,$im_wdth-$mrgn,$y,$line_clr);
    		$v=intval($horizontal_gap * $i /$ratio);
    		imagestring($img,0,5,$y-5,$v,$color_bar);

	}


	# ------PLOTTING THE GRAPH USING BARS------
	for($i=0;$i< $bar_numbr; $i++)
	{ 
    		# ------ Extract key and value pair from the current pointer position
    		list($key,$value)=each($values); 
    		$x1= $mrgn + $gap + $i * ($gap+$bar_wth) ;
    		$x2= $x1 + $bar_wth; 
    		$y1=$mrgn +$gr_ht- intval($value * $ratio) ;
    		$y2=$im_ht-$mrgn;
    		imagestring($img,0,$x1+3,$y1-10,$value,$color_bar);imagestring($img,0,$x1+3,$im_ht-15,$key,$color_bar);        
    		imagefilledrectangle($img,$x1,$y1,$x2,$y2,$color_bar);
	}
 	$chart_name = "chart.png"; imagepng($img, $chart_name,0); 
	$_REQUEST['asdfad']=234234;
	$html = '<h3>Name Search for '.$name.' </h3>
	<img src="chart.png" name="chart" />';
	$dom = new DOMDocument;
	$dom->loadHTML($html);
	echo $dom->saveHTML();
	}
}
?>
<br>
<br></DIV>
</CENTER>

<BR>
<BR><BR>
<BR>
<DIV ID="FOOTER">

<H2>DO VISIT AGAIN </H2>
</DIV>
</BODY>
</HTML>
