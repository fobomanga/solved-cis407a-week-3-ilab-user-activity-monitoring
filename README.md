Download Link: https://assignmentchef.com/product/solved-cis407a-week-3-ilab-user-activity-monitoring
<br>
<header class="entry-header"></header>

5/5 - (2 votes)

In this lab, we will demonstrate how to save user activity data in a database. We will be creating a new form to display the user activity data, a new dataset to contain the data, a data access class to structure the code, and a function within the data access class to save users’ activity data when users visit the Personnel form page (frmPersonnel.aspx). We will also be adding server side validation to the frmPersonnel for you added in the previous lab and update or main menu for the new functionality. INCLUDE A SCREENSHOT OF THE ASSIGNMENT SUCCESSFULLY RUNNING TO RECEIVE CREDIT

<strong>Deliverables</strong>All files are located in the subdirectory of the project. The project should function as specified: When you visit the Personnel form page (frmPersonnel.aspx), a record should be saved in the tblUserActivity table with the IP address, form name accessed (frmPersonnel), and the date accessed. When you click the “View Activity” button, you should see at least one record with this information. When the user goes to the frmPersonnel web form and enters data the following business rules are to be enforced:• Fields may not be empty or filled with spaces. If any field is empty, turn that field background color to yellow and add to/create an error message to be shown in the error label.• The end date must be greater than the start date. If the end date is less than the start date turn both date fields yellow and add to/create an error message to be shown in the error label.If all fields validate properly, then the session state items should be set properly and the user should see the frmPersonnelVerified form with all the values displayed. You will also add a new item to frmMain that will take the user to the new frmUserActivity form you added. Add the proper link and a hyperlinked image to allow the user to select this new option. Once you have verified that everything works, save your website, zip up all files, and submit in the Dropbox.

<strong>iLAB STEPS</strong><strong>STEP 1:</strong> Data Connection, Dataset and Data Access Class (10 points)1. Open Microsoft Visual Studio.NET 2008.2. Open the PayrollSystem website by clicking on it in the Recent Projects list, or by pulling down the File menu, selecting Open Website, navigating to the folder where you previously saved the PayrollSystem, and clicking Open.3. Download the PayrollSystem_DB.MDB file from Doc Sharing and save it on your local computer. (Note: your operating system may lock or block the file. Once you have copied it locally, right click on the file and select Properties and then Unblock if available). Then add it to the PayrollSystem website as follows: In Visual Studio, in the Solution Explorer click Website, Add Existing Item, then navigate to the PayrollSystem_DB.MDB file you downloaded and click the Add button.4. Now we need to create a new connection to the PayrollSystem_DB.MDB. To begin, click View Server Explorer.5. When the Server Explorer toolbox appears, click the Connect to Database button.6.When the Add Connection dialog appears, click the Change button. In the “Change Data Source” dialog, select MS Access Database File; Uncheck Always use this Selection; then click OK.7. Click the Browse button to navigate to the PayrollSystem_DB.mdb file in your website folder, then click “Open”. (NOTE: Be sure you select the PayrollSystem_DB.mdb file in your PayrollSystem website folder, not the one you originally downloaded from Doc Sharing!) Click Test Connection. You should receive a message that the test connection succeeded. Click OK to acknowledge the message, then click “OK” again to close the Add Connection dialog.8. The PayrollSystem_DB.mdb should be added to the Server Explorer. Expand the database, then expand the Tables entry under the database until you see tblUserActivity. Leave the Server Explorer window open for now as you will be returning to it in a moment.9. Create a new dataset by selecting Website Add New Item. Under Templates, select the Dataset item. Enter dsUserActivity.xsd for the name. Click Add.10. Click here for text discription of this image.11. If the following message appears, select Yes. You want to make this dataset available to your entire website.12. If the TableAdapter Configuration Wizard dialog appears, click Cancel. (We will be configuring a Data Adapter for this dataset later in C# code, so we do not need to run this wizard.)13. Drag-and-drop the tblUserActivity table from the Server Explorer window into the dsUserActivity dataset in the editor window.NOTE: If you see a message that says your connection uses a local data file that is not in the current project, that indicates you did not select the correct PayrollSystem_DB.mdb file when you created your data connection. To fix this problem, click No, then right-click on PayrollSystem_DB.mdb in the Server Explorer window and choose Modify Connection. Click the Browse button, navigate to the PayrollSystem_DB.mdb file that is in your PayrollSystem website folder, and click Open. Test the connection, then click OK.14. Click the Save icon on the toolbar to save the dsUserActivity.xsd dataset.15. Click here for text discription of this image.16. (You can now close the Server Explorer window if you wish.)17. Create a new class to contain the C# code that will access this dataset. To do so, click Website, Add New Item. In the Add New Item dialog, select the Class template, and enter clsDataLayer for the name. Make sure the Language is set to Visual C#. Click “Add”.18. Click here for text discription of this image.19. If the following message appears, select Yes. You want to make this class available to everything in your solution.20. Add the following to the top of your class, below any other using statements created for you by Visual Studio:

21. Add the following three functions inside the squiggly braces for the “public class clsDataLayer” class, above the beginning of the “public clsDataLayer()” constructor:

<strong>STEP 2:</strong> frmUserActivity, frmPersonnel, frmMain (10 points)18. Create a new Web form called frmUserActivity. Switch to Design Mode and add a Label and GridView (found under the Toolbox, Data tab) having the following properties:Property ValueLabel – Text User ActivityGridView – (ID) grdUserActivity19. Go to the Page_Load method and add the following code:

20. Open the frmMain form, add a new link button and image button to point to the new frmUserActivity. Find an image to use for the image button and add the new option as View User Activity.21. Go to the frmMain Page_Load and add the following code:

22. On the frmUserActivity form, add the CoolBiz logo hyperlinked logo at the top of the page so that when clicked the user is returned to frmMain.23. In the Solution Explorer, right click on the frmMain.aspx form and select Set As Start Page. Run your project. When you open the project, a record should be saved in the tblUserActivity table with the IP address, form name accessed (frmPersonnel), and the date accessed. When you click the View Activity button, you should see at least one record with this information.24. You will now add server side validation code to the frmPersonnel page. Currently, when the Submit button is pressed, the frmPersonnelVerified page is displayed. This is because the frmPersonnelVerified page is set as the Submit button’s PostBackUrl property. Instead of having the page go directly to the frmPersonnelVerified page when the Submit button is pressed, we want to do some server side validation. If any of the validation rules fail, we will redisplay the frmPersonnel page with the fields in question highlighted in yellow with an error message displayed.First, it is important to understand what is currently happening when the submit button is pressed. This is causing a postback of the form to the frmPersonnelVerified form. When this postback happens, all of the data in the fields on the frmPersonnel form are sent to the frmPersonnelVerified form as name value pairs. In the Page_Load code of frmPersonnelVerified these values are picked up from the Request object and displayed. Each name value pair will be in the Request object as the ID of the control containing the value and the value itself. We can pass data between pages by using Session state instead. In order to do validation on the values but still have the values visible on the frmPersonnelVerified page, we will need to change not only the PostBack URL of the frmPersonnel page but also how the frmPersonnelVerified form is getting the data – it will need to get it from Session state rather than from the Request object.

Make the following changes:1. Clear the Submit button PostBackURLProperty on the frmPersonnel form.2. In the btnSubmit_Click event handler get each value from the data entry fields and set Session state items for each.3. Change the frmPersonnelVerified code behind to get the values from the Session state items you created in the previous step.When you are done with these steps, you should be able to enter data on the frmPersonnel data entry form and then click the Submit button. The frmPersonnelVerified page should then be displayed with the values that were in the data entry fields on frmPersonnel.Make sure this is all working before proceeding to the next steps.25. Add a label to the frmPersonnel form with an ID of lblError. Do not place the label to the right or left of any of the controls on the form. Add it below the controls or above the controls. The text property of this label should be set to an empty string.26. Add code to perform server side validation in response to the submit button being clicked. Here are the business rules we want to enforce (remember this will be server C# code in the frmPersonnel code behind): Fields may not be empty or filled with spaces. If any field is empty, turn that field background color to yellow and add to/create an error message to be shown in the error label. The end date must be greater than the start date. If the end date is less than the start date, turn both date fields yellow and add to/create an error message to be shown in the error label. If all fields validate properly then the session state items should be set properly and the user should see the frmPersonnelVerified form with all the values displayed.27. Lab Hints: To set a value in session state do the following:

28. “txtFirstName” is the key and txtFirstName.Text is the value.29. To get this same value back from the session we use the key and the Session object as follows:

30. There is a Trim method on the string object that will automatically remove spaces from the beginning and end of a string. Remember, you can turn an object like a Session item object into a string using the Convert class or just using it’s ToString() method.31. You may want to create variables to work with for validation rather than using the Request item objects directly.32. To turn a string into a DateTime object you can use the DateTime method Parse. If you had a date value stored in a string called strDate, you could turn it into a DateTime object like this:

33. You can compare two DateTime objects by using the DateTime.Compare method. If you had two DateTime objects called dt1 and dt2 you can check to see if dt1 is greater than dt2 by doing this:

34. DateTime.Compare will return a 0 if the two dates are equal, a 1 if dt1 is greater than dt2, and a -1 if dt1 is less than dt2.35. If you put in an invalid date for either of the date fields, you will get an exception/server error when trying to parse the values. We will address this in a later lab – for now make sure you enter valid dates (valid meaning a date in the form of mm/dd/yyyy).36. If I had a TextBox control that was called txtAge and you wanted to set it’s background color you could do this:

37. Remember to clear the PostBackURL property of the submit button!

<strong>STEP 3:</strong> Verify and submit (10 points)28. View the video above on what functions your lab should have so far.29. Run your project. When you open the project, and go to the main menu form a record should be saved in the tblUserActivity table with the IP address, form name accessed (frmPersonnel), and the date accessed. When you click the View Activity button you should see at least one record with this information. The validation and error display should work for entering data. All navigation and hyperlinks should work.Once you have verified that it works, save your project, zip up all files, and submit in the Dropbox.

<strong>NOTE:</strong> Make sure you include comments in the code provided where specified (where the ” //Your comments here” is mentioned) and for any code you write, or else a five point deduction per item (form, class, function) will be made. You basically put two forward slashes, which start the comment; anything after the // on that line is disregarded by the compiler. Then type a brief statement describing what is happening in following code. Comments show professionalism and are a must in systems. As a professional developer, comments will set you apart from others and make your life much easier if maintenance and debugging are needed.

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php comments">// Add your comments here</code>

<code class="php plain">using System.Data.OleDb;</code>

<code class="php plain">using System.Net;</code>

<code class="php plain">using System.Data;</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php comments">// This function gets the user activity from the tblUserActivity</code>

<code class="php keyword">public</code> <code class="php keyword">static</code> <code class="php plain">dsUserActivity GetUserActivity(string Database)</code>

<code class="php plain">{</code>

<code class="php comments">// Add your comments here</code>

<code class="php plain">dsUserActivity DS;</code>

<code class="php plain">OleDbConnection sqlConn;</code>

<code class="php plain">OleDbDataAdapter sqlDA;</code>

<code class="php comments">// Add your comments here</code>

<code class="php plain">sqlConn = </code><code class="php keyword">new</code> <code class="php plain">OleDbConnection(</code><code class="php string">"PROVIDER=Microsoft.Jet.OLEDB.4.0;"</code> <code class="php plain">+</code>

<code class="php string">"Data Source="</code> <code class="php plain">+ Database);</code>

<code class="php comments">// Add your comments here</code>

<code class="php plain">sqlDA = </code><code class="php keyword">new</code> <code class="php plain">OleDbDataAdapter(</code><code class="php string">"select * from tblUserActivity"</code><code class="php plain">, sqlConn);</code>

<code class="php comments">// Add your comments here</code>

<code class="php plain">DS = </code><code class="php keyword">new</code> <code class="php plain">dsUserActivity();</code>

<code class="php comments">// Add your comments here</code>

<code class="php plain">sqlDA.Fill(DS.tblUserActivity);</code>

<code class="php comments">// Add your comments here</code>

<code class="php keyword">return</code> <code class="php plain">DS;</code>

<code class="php plain">}</code>

<code class="php comments">// This function saves the user activity</code>

<code class="php keyword">public</code> <code class="php keyword">static</code> <code class="php plain">void SaveUserActivity(string Database, string FormAccessed)</code>

<code class="php plain">{</code>

<code class="php comments">// Add your comments here</code>

<code class="php plain">OleDbConnection conn = </code><code class="php keyword">new</code> <code class="php plain">OleDbConnection(</code><code class="php string">"PROVIDER=Microsoft.Jet.OLEDB.4.0;"</code> <code class="php plain">+</code>

<code class="php string">"Data Source="</code> <code class="php plain">+ Database);</code>

<code class="php plain">conn.Open();</code>

<code class="php plain">OleDbCommand command = conn.CreateCommand();</code>

<code class="php plain">string strSQL;</code>

<code class="php plain">strSQL = </code><code class="php string">"Insert into tblUserActivity (UserIP, FormAccessed) values ('"</code> <code class="php plain">+</code>

<code class="php plain">GetIP4Address() + </code><code class="php string">"', '"</code> <code class="php plain">+ FormAccessed + </code><code class="php string">"')"</code><code class="php plain">;</code>

<code class="php plain">command.CommandType = CommandType.Text;</code>

<code class="php plain">command.CommandText = strSQL;</code>

<code class="php plain">command.ExecuteNonQuery();</code>

<code class="php plain">conn.Close();</code>

<code class="php plain">}</code>

<code class="php comments">// This function gets the IP Address</code>

<code class="php keyword">public</code> <code class="php keyword">static</code> <code class="php plain">string GetIP4Address()</code>

<code class="php plain">{</code>

<code class="php plain">string IP4Address = string.</code><code class="php functions">Empty</code> <code class="php plain">;</code>

<code class="php keyword">foreach</code> <code class="php plain">(IPAddress IPA in</code>

<code class="php plain">Dns.GetHostAddresses(HttpContext.Current.Request.UserHostAddress)) {</code>

<code class="php keyword">if</code> <code class="php plain">(IPA.AddressFamily.ToString() == </code><code class="php string">"InterNetwork"</code><code class="php plain">) {</code>

<code class="php plain">IP4Address = IPA.ToString();</code>

<code class="php keyword">break</code><code class="php plain">;</code>

<code class="php plain">}</code>

<code class="php plain">}</code>

<code class="php keyword">if</code> <code class="php plain">(IP4Address != string.</code><code class="php functions">Empty</code><code class="php plain">) {</code>

<code class="php keyword">return</code> <code class="php plain">IP4Address;</code>

<code class="php plain">}</code>

<code class="php keyword">foreach</code> <code class="php plain">(IPAddress IPA in Dns.GetHostAddresses(Dns.GetHostName())) {</code>

<code class="php keyword">if</code> <code class="php plain">(IPA.AddressFamily.ToString() == </code><code class="php string">"InterNetwork"</code><code class="php plain">) {</code>

<code class="php plain">IP4Address = IPA.ToString();</code>

<code class="php keyword">break</code><code class="php plain">;</code>

<code class="php plain">}</code>

<code class="php plain">}</code>

<code class="php keyword">return</code> <code class="php plain">IP4Address;</code>

<code class="php plain">}</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php keyword">if</code> <code class="php plain">(!Page.IsPostBack) {</code>

<code class="php comments">// Declares the DataSet</code>

<code class="php plain">dsUserActivity myDataSet = </code><code class="php keyword">new</code> <code class="php plain">dsUserActivity();</code>

<code class="php comments">// Fill the dataset with what is returned from the function</code>

<code class="php plain">myDataSet = clsDataLayer.GetUserActivity(Server.MapPath(</code><code class="php string">"PayrollSystem_DB.mdb"</code><code class="php plain">));</code>

<code class="php comments">// Sets the DataGrid to the DataSource based on the table</code>

<code class="php plain">grdUserActivity.DataSource = myDataSet.Tables[</code><code class="php string">"tblUserActivity"</code><code class="php plain">];</code>

<code class="php comments">// Binds the DataGrid</code>

<code class="php plain">grdUserActivity.DataBind();</code>

<code class="php plain">}</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php comments">// Add your comments here</code>

<code class="php plain">clsDataLayer.SaveUserActivity(Server.MapPath(</code><code class="php string">"PayrollSystem_DB.mdb"</code><code class="php plain">), </code><code class="php string">"frmPersonnel"</code><code class="php plain">);</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php plain">Session[</code><code class="php string">"txtFirstName"</code><code class="php plain">] = txtFirstName.Text;</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php plain">Session[</code><code class="php string">"txtLastName"</code><code class="php plain">].ToString()</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php plain">DateTime myDateTimeObject = DateTime.Parse(strDate);</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>

<code class="php keyword">if</code> <code class="php plain">(DateTime.Compare(dt1,dt2) &gt; 0)</code>

<table border="0" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td class="code"></td>

  </tr>

 </tbody>

</table>