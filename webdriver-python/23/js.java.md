执行js
=======

场景
----
如果你熟悉js的话，那么使用webdriver执行js就是一件很高效的事情了。在webdriver脚本中直接执行js的好处很多，这里就不一一枚举了。

webdriver提供了JavascriptExecutor(dr).executeScript()接口来帮助我们完成这一工作。在实际的测试脚本中，以下两种场景是经常遇到的

* 在页面直接执行一段js
* 在某个已经定位的元素的上执行js

代码
----
下面的代码演示了如何在页面以及在已经定位的元素上执行js

### js.html
```
  <html>
    <head>
      <meta http-equiv="content-type" content="text/html;charset=utf-8" />
      <title>js</title>		
      <script type="text/javascript" async="" src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
      <link href="http://netdna.bootstrapcdn.com/twitter-bootstrap/2.3.2/css/bootstrap-combined.min.css" rel="stylesheet" />		
      <script type="text/javascript">
        $(document).ready(function(){
          $('#tooltip').tooltip({"placement": "right"});
        });
      </script>
    </head>
      
    <body>
      <h3>js</h3>
      <div class="row-fluid">
        <div class="span6 well">		
          <a id="tooltip" href="#" data-toggle="tooltip" title="watir-webdriver better than selenium-webdriver">hover to see tooltip</a>
          <a class="btn">Button</a>
        </div>		
      </div>		
    </body>
    <script src="http://netdna.bootstrapcdn.com/twitter-bootstrap/2.3.2/js/bootstrap.min.js"></script>
  </html>

```

### js.java
```
	import java.io.File;
	import java.util.List;

	import org.openqa.selenium.Alert;
	import org.openqa.selenium.By;
	import org.openqa.selenium.JavascriptExecutor;
	import org.openqa.selenium.Keys;
	import org.openqa.selenium.WebDriver;
	import org.openqa.selenium.WebElement;
	import org.openqa.selenium.chrome.ChromeDriver;


	public class Js {

		public static void main(String[] args) throws InterruptedException {
			WebDriver dr = new ChromeDriver();
			
			File file = new File("src/js.html");
			String filePath = "file:///" + file.getAbsolutePath();
			System.out.printf("now accesss %s \n", filePath);
			
			dr.get(filePath);
			Thread.sleep(1000);
			
	//		在页面上直接执行js
			((JavascriptExecutor)dr).executeScript("$('#tooltip').fadeOut();");
			Thread.sleep(1000);
			
	//		在已经定位的元素上执行js
			WebElement button = dr.findElement(By.className("btn"));
			((JavascriptExecutor)dr).executeScript("$(arguments[0]).fadeOut();", button);
				
			
			Thread.sleep(1000);
			System.out.println("browser will be close");
			dr.quit();	
		}

	}
```

