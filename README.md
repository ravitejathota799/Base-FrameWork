# Base-FrameWork

This is a base framework for the projects:

**Encapsulation:**
---------------------------------------------------------------------------------------------------------------------------------
Meaning: Restrict direct access to fields and provide controlled access.
Example: Private web elements with public action methods.
public class LoginPage {
 private WebElement un;
 private WebElement pwd;
public void enterUsername(String username) { 
 un.sendKeys(username); }
public void enterPassword(String password) { 
 pwd.sendKeys(password); }
}
👉 Tip: Always keep page elements private and expose only actions for better security and maintenance.
**Inheritance:**
---------------------------------------------------------------------------------------------------------------------------------
Meaning: Reuse common functionality across classes.
Example: Page classes inherit driver setup via PageFactory.
public class BasePage {
 protected WebDriver driver;
public BasePage(WebDriver driver) {
 this.driver = driver;
 PageFactory.initElements(driver, this);
 }
}
public class HomePage extends BasePage {
 public HomePage(WebDriver driver) {
 super(driver);
 }
}
👉 Tip: Centralizing driver and element initialization keeps your page classes clean and DRY!
**Polymorphism (Overloading):**
Meaning: Same method name, different input parameters (compile-time polymorphism).
Example: Overloaded Actions methods.
Actions actions = new Actions(driver);
actions.moveToElement(element).perform();
actions.moveToElement(element, 50, 50).click().perform();
👉 Tip: Method Overloading gives flexibility when interacting with elements dynamically!
**Polymorphism (Overriding):**
Meaning: Subclass modifies parent class behavior (runtime polymorphism).
Example: Custom RetryAnalyzer overriding retry behavior in TestNG.
public class RetryAnalyzer implements IRetryAnalyzer {
 private int retryCount = 0;
 private static final int maxRetryCount = 2;
 @Override
 public boolean retry(ITestResult result) {
 if (retryCount < maxRetryCount) {
 retryCount++;
 return true;
 }
 return false;
 }
}
👉 Tip: Overriding retry() lets you control how many times failed tests are automatically retried!
**Abstraction:**
Meaning: Hide complex logic and expose simple actions to the user.
Example: Abstract Base Test class for browser setup/teardown.
// Abstract class
public abstract class Browser {
 WebDriver driver;
 // Abstract method - no body
 public abstract void openBrowser();
 }
}
 Concrete Subclasses:
public class ChromeBrowser extends Browser {
 @Override
 public void openBrowser() {
 driver = new ChromeDriver();
 System.out.println("Chrome Browser Opened!");
 }
}
Abstract Class = "What should happen" (rules)
Concrete Class = "How it happens" (details)
👉 Tip: Abstraction simplifies your framework — Test classes focus only on testing, not setup details!
