
/*
vbcrlf				:	空一格	
Globals!TotalPages 	: 	RDLC整各頁數
Globals!PageNumber 	: 	1表示第一頁 

*/





//如何快速建立DataSet
DataSet ds = new DataSet("SCM270R");
ds.Tables.Add(dt);
ds.WriteXmlSchema("D:\\SCM270R.xsd");


//轉字串並且符合數值格式
=　Format(Fields!UBRD_ScrapValue1.Value,"N0") 


=iif( ( Parameters!StampKind.Value="1" 
		or (Parameters!StampKind.Value="2" and Globals!PageNumber = Globals!TotalPages) 
	    or (Parameters!StampKind.Value="3" and Globals!PageNumber = 1)),false,true)



=Replace(Fields!ADD_AMOUNT.Value,"\n",vbcrlf)

=IIF(Fields!IsAll.Value = "True","是","否")

=CountRows()  [取欄位個數]

=RowNumber([colname])

=Int((RowNumber("colname")-1)/12)       //群組分頁,12表示12筆一頁


//西元年
= Format(Globals!ExecutionTime,"yyy/MM/dd")

//日期(民國年)
= Format(Globals!ExecutionTime.AddYears(-1911),"yyy/MM/dd")

//頁碼
=(Globals!PageNumber).ToSTRing() +"-"+ (Globals!TotalPages).tostring()

//判斷是否有資料
=IIf(RowNumber(Nothing)=0,"＊＊無資料＊＊","")

=Switch(Parameters!P_Sys.Value="1","地址",Parameters!P_Sys.Value="2","使用分區",Parameters!P_Sys.Value="3","使用分區")

=Right(Fields!PAGETYPE.Value, 3)

=Fields!UMMD_Specification_XX.Value  & iif(Fields!UMMD_LicensePlate.Value="" ,"", "/" & Fields!UMMD_LicensePlate.Value)


1.新增群組，輸入下面公式 =Int((RowNumber(NOTHING)-1)/35) 35筆一頁
2.群組的分頁符號選項勾選"在群組的每個執行個體之間"

若要拆成5筆資料一條黑線
在BorderStyle的Bottom公式輸入 =IIf(RowNumber("K01") mod 5 =0,"Double","None")即可


=Ceiling(RowNumber("Group")/10)

