---
layout: post
published: true
mathjax: false
featured: false
imagefeature: cover1.jpg
comments: false
title: Page Object Model
categories:
  - Testing
modified: '2018-02-12'
description: Introduction of the Page Object Model
tags: test
---
# 1. Problem

Starting an UI Automation in Selenium WebDriver is NOT a tough task. You just need to find elements, perform operations on it.

The chief problem with script maintenance is that if 10 different scripts are **using the same page element**, with **any change** in that element, you **need to change all 10 scripts**. This is time consuming and error prone.

# 2. Idea

A better approach to script maintenance is to create a **separate class file** which would find web elements, fill them or verify them. This class can be **reused** in all the scripts using that element. 

In future, if there is a change in the web element, we need to make the change in **just 1 class file** and not 10 different scripts.

This approach is called Page Object Model(POM). It helps make the code more readable, maintainable, and reusable.

# 3. POM

Page Object Model is a **design pattern** to create Object Repository for web UI elements. 
Under this model, for each web page in the application, there should be corresponding page class.

This Page class will find the WebElements of that web page and also contains Page methods which perform operations on those WebElements. 

Name of these methods should be given as per the task they are performing, i.e., if a loader is waiting for the payment gateway to appear, POM method name can be waitForPaymentScreenDisplay().

# 4. Advantages of POM

- Page Object Patten says operations and flows in the UI should be separated from verification. This concept makes our code cleaner and easy to understand.
- The Second benefit is the object repository is independent of test cases, so we can use the same object repository for a different purpose with different tools. For example, we can integrate POM with TestNG/JUnit for functional Testing and at the same time with JBehave/Cucumber for acceptance testing.
- Code becomes less and optimized because of the reusable page methods in the POM classes. 
Methods get more realistic names which can be easily mapped with the operation happening in UI. i.e. if after clicking on the button we land on the home page, the method name will be like 'gotoHomePage()'.

**StartPage.java**
{% highlight java linenos %}package pom.example.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

public class StartPage {
	WebDriver driver;
	
	By byFieldZip = By.xpath("//form[@id='quoteForm']/p/input");
	By bySendButton = By.id("submitButton");
	
	public StartPage( WebDriver driver ) {
		this.driver = driver;
	}
	
	public void setFieldZip(String zip) {		
		WebElement elementFieldZip = driver.findElement( byFieldZip );
		elementFieldZip.sendKeys("22030");
	}
	
	public void clickOnSendButton() {		
		WebElement elementSendButton = driver.findElement( bySendButton );
		elementSendButton.click();
	}
	
	public void startPage(String zip) {
		setFieldZip(zip);
		clickOnSendButton();
	}
}{% endhighlight %}

**DataPage.java.java**
```java
package pom.example.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class DataPage {
	WebDriver driver;

	By byCityField = By.id("cityState");
	
	public DataPage( WebDriver driver ) {
		this.driver = driver;
		
		//Explicit Waiting until the cityState field appears in the DOM
		WebDriverWait wait = new WebDriverWait( driver, 10);				
		wait.until(ExpectedConditions.visibilityOfAllElementsLocatedBy(byCityField ));
	}
	
	public String getTextFromCityField() {
		WebElement elementCityField = driver.findElement( byCityField );
		JavascriptExecutor jse = (JavascriptExecutor)driver;
		String stringCity = (String) jse.executeScript("return arguments[0].value", elementCityField);
		return stringCity;		
	}	
}
```

**TestSuit01.java**
```java
package pom.example.test;

import static org.junit.Assert.assertEquals;
import java.util.concurrent.TimeUnit;
import org.junit.AfterClass;
import org.junit.BeforeClass;
import org.junit.Test;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import pom.example.pages.DataPage;
import pom.example.pages.StartPage;

public class TestSuit01 {
	static final String START_URL = "http://geico.com";
	static final String zipCode = "22030";
	static final String cityName = "Fairfax, VA";
	
	static WebDriver driver;
	static StartPage startPage;
	static DataPage dataPage;
	
	@BeforeClass
	public static void setup(){
		driver = new ChromeDriver();		
		driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS );
	}
	
	@Test
	public void testCase01() {
		driver.get(START_URL);
		
		//--- StartPage ---
		startPage = new StartPage( driver );
		startPage.startPage( zipCode );
		
		//--- DataPage ---
		dataPage = new DataPage( driver );
		String gainedCity = dataPage.getTextFromCityField();
		assertEquals("The gained city is not the expected: ", cityName, gainedCity);
		
	}	
	
	@AfterClass
	public static void tearDown() {
		driver.close();
	}
}
```

