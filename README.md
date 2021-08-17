# create table with field clob
CREATE TABLE TABELA (ID INTEGER PRIMARY KEY,
					 FIELD_CLOB CLOB);

# read file and insert field clob 

if (file_exists("insert path". $FILE_NAME)) {
	$file = fopen("insert path".$FILE_NAME, 'rw') or die ("Unable to open file!");
	while(!feof($file)) 
	{
		if ($count2 < 500 ){
			$Char1 = fgetc($file);
			$caracteres .= $Char1;
			$count2++;
		} else {
			$sql = parent::sql("UPDATE TABELA SET FIELD_CLOB = FIELD_CLOB || '" .$caracteres. "'  WHERE ID = ".$ID."");
			$caracteres = '';
			$count2 = 0;
		}
		if (feof($file)) {
			$sql = parent::sql("UPDATE TABELA SET FIELD_CLOB = FIELD_CLOB || '" .$caracteres. "'  WHERE ID = ".$ID."");
		}
	}
}




# select field clob 
$result = parent::sql("SELECT ID, 
		to_char(substr(FIELD_CLOB, 0, 4000)) AS file_content, 
		to_char(substr(FIELD_CLOB, 4001, 4000)) AS file_content2, 
		to_char(substr(FIELD_CLOB, 8000, 4000)) AS file_content3, 
		to_char(substr(FIELD_CLOB, 12000, 4000)) AS file_content4
		from TABELA WHERE ID = ".$id); 
# list content select  		
		$FILE_CONTENT    = $result[0]->FILE_CONTENT; 
		$FILE_CONTENT2   = $result[0]->FILE_CONTENT2; 
		$FILE_CONTENT3   = $result[0]->FILE_CONTENT3;
		$FILE_CONTENT4   = $result[0]->FILE_CONTENT4;
		
return json_encode($result);
