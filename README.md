# Selenium-
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import java.time.Duration;

public class fitpeo {
    public static void main(String[] args) {
        System.setProperty("webdriver.gecko.driver", "C:\\\\Users\\\\hp\\\\eclipse-workspace\\\\project 1\\\\SeleniumDemo1\\\\Resources\\\\geckodriver.exe");
        WebDriver driver = new FirefoxDriver();

        try {
            driver.get("https://www.fitpeo.com");
            driver.manage().window().maximize();

            WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(20));
            WebElement calculatorLink = wait.until(ExpectedConditions.elementToBeClickable(By.linkText("Revenue Calculator")));
            calculatorLink.click();

            WebElement slider = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("slider-id"))); // Adjust locator
            new Actions(driver).moveToElement(slider).perform();

            int desiredValue = 820;
            int sliderWidth = slider.getSize().width;
            int xOffset = (sliderWidth * desiredValue) / 1000;
            new Actions(driver).dragAndDropBy(slider, xOffset, 0).perform();

            WebElement textField = driver.findElement(By.id("text-field-id")); // Adjust locator
            textField.clear();
            textField.sendKeys("560");

            driver.findElement(By.id("cpt-99091")).click(); // Adjust locators
            driver.findElement(By.id("cpt-99453")).click();
            driver.findElement(By.id("cpt-99454")).click();
            driver.findElement(By.id("cpt-99474")).click();

            WebElement reimbursement = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("reimbursement-id"))); // Adjust locator
            String reimbursementText = reimbursement.getText();
            if (reimbursementText.equals("$110700")) {
                System.out.println("Total Recurring Reimbursement validation passed.");
            } else {
                System.out.println("Total Recurring Reimbursement validation failed.");
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            driver.quit();
        }
    }
}

