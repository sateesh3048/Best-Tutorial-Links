

## How to open browser automatically in intellij

To make the browser start automatically when you run the Spring Boot app in IntelliJ Community Edition, you can follow these steps:

1. Open the Run/Debug Configuration dialog by clicking on the drop-down arrow next to the green Run button in the toolbar and selecting "Edit Configurations".

2. In the dialog, select the Spring Boot configuration you want to modify.

3. In the "Before Launch" section, click the "+" button and select "Run External Tool".

4. In the "Tool Settings" dialog, click the "+" button to add a new tool.

5. In the "Create Tool" dialog, enter a name for the tool (e.g. "Open Browser") and select "Browser" as the tool type.

6. In the "Browser Settings" section, enter the URL you want to open in the browser (e.g. "http://localhost:8080/") and select the browser you want to e.

7. Click "OK" to save the tool and close the dialog.

8. Back in the "Run/Debug Configuration" dialog, move the new "Run External Tool" item to the top of the list by clicking the up arrow button.

9. Click "OK" to save the configuration.

Now, when you run the Spring Boot app, IntelliJ will automatically open the specified URL in the selected browser.



## Add Json pretty print addon to see json in the best way!

