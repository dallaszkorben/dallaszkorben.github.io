---
layout: post
published: true
mathjax: false
featured: true
comments: true
title: Page Object Model
modified: '2018-03-07'
description: Introduction of the Page Object Model
blog: testing
category: [Automation]
tags: [Testing, Automation]
---
# 1. Introduction

Everybody facing a serious problem who starts to automate a page. It happens that you have to test the same page (or only some elements on the page) in `different test cases` (or even different test types).
The point is that an element on a page can have more than one reference in the code.

Why is it a problem? Well, that means that normally you use the `same locator` to identify the same element, which is hard coded, `more than once`.
This is bad practice of course and it hurts the DRY (Don't Repeat Yourself)/DIE (Duplication Is Evil) principle.

What if the locator changes on the page? You have to fix all locators in the code. This is time consuming and there is a big chance of not finding all.

# 2. Idea

A better approach to script maintenance is to create a `separate class file` which would **find** web elements, **fill** them or **verify** them. This class can be `reused` in all the scripts using that element. 

In future, if there is a change in the web element, we need to make the change in `just 1 class file`.

This approach is called `Page Object Model(POM)`. It helps make the code more readable, maintainable, and reusable.

# 3. Conclusion - POM

**Page Object Model** is a `design pattern` to create **Object Repository** for web UI elements. 

Under this model, each `web page` in the application should have a corresponding `page class`.

This Page class contains identificators which `find the WebElements` of that web page and also contains Page methods which `perform operations` on those WebElements. 

Name of these methods should be given as per the task they are performing, i.e., if a loader is waiting for the payment gateway to appear, POM method name can be waitForPaymentScreenDisplay().

# 4. Advantages of POM

- Page Object Patten says **operations** and **flows** in the UI should be separated from verification. This concept makes our code cleaner and easy to understand.
- The **object repository** is `independent` of test **cases**, so we can use the same object repository for a different purpose with different tools. For example, we can integrate POM with TestNG/JUnit for functional Testing and at the same time with JBehave/Cucumber for acceptance testing.
- `Code becomes less` and `optimized` because of the reusable page methods in the POM classes. 
- Methods get more **realistic names** which can be `easily mapped` with the operation happening in UI. i.e. if after clicking on the button we land on the home page, the method name will be like 'gotoHomePage()'.

# 5. An example

In this chapter I show a simple example which demonstrates the `POM`.
The **TestSuit01.java** file represents the Test Suit which contains Test Cases.
This file does not have any locator or low-level operation.

The **StartPage.java** represents the first page and the **DataPage.java.java** represents the second page of the site which we want to test.
They define the `locators` as **xpath** and **id** and some low-leve operations as **setField()** or **clickOnButton()**. Besides that there are high-level operations defined here as well which affects the behaviour of the entire page. For example fillOutAllField() with specific data. Typically the Test Cases call this methods.


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
{% highlight java linenos %}package pom.example.pages;

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
{% endhighlight %}

**TestSuit01.java**
{% highlight java linenos %}package pom.example.test;

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
{% endhighlight %}
