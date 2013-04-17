YiiFusioncharts
===============

FusionCharts extension for Yii - using FusionCharts free

Userful resources:
- http://docs.fusioncharts.com/free/

Installation:

- copy FusionCharts folder to protected/Extentsion folder on Yii project
- copy FusionCharts.js file to js folder
- copy Charts folder to root directory
- add the code below  to import module in Yii config file.

```php
	'application.extensions.FusionCharts.*'
```
 
- add js file to the project by adding the code below in your view:

```php
	Yii::app()->clientScript->registerScriptFile("/js/FusionCharts.js", CClientScript::POS_HEAD );
```  
 
- example of using FusionChart:

```php
  $sql = "SELECT date, sum(download) downloads"
	." FROM `download`"
	." where date >= ".$startdate
	." and date < ".$enddate
	." group by date"
	." order by date"
	."";
	
 $command = $connection->createCommand($sql);
 
 $rows = $command->queryAll();
 
 $strXML2 = "<graph caption='Downloads Broken down by date' formatNumberScale='0' decimalPrecision='0' >";
 
 $fusionChart2 = new FusionCharts;
 
 foreach ($rows as $row){
 	$strXML2 .= "\<set name='".date('d/m/Y', $row['date']). "' value='".$row['downloads']."' color='" .FusionChartUtils::getFCColor($count++) . "'\>\</set\>";
 }
 
 $strXML2 .= "</graph>";
 
 echo $fusionChart2->renderChart("/FusionCharts/FCF_Column3D.swf", "", $strXML2, "Downloads Graph", 600, 400);
```
