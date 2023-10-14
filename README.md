# AutoWebViva
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.Select;

public class VivacomPage {
    private WebDriver driver;

    public VivacomPage(WebDriver driver) {
        this.driver = driver;
    }

    // Existing methods from the previous script...

    public void chooseDevice(String deviceName) {
        WebElement device = driver.findElement(By.xpath("//div[contains(@class, 'product-card') and contains(text(), '" + deviceName + "')]"));
        device.click();
    }

    public void chooseMobilePlan(String planName, String paymentOption) {
        WebElement mobilePlanDropdown = driver.findElement(By.id("MobilePlan"));
        Select planSelect = new Select(mobilePlanDropdown);
        planSelect.selectByVisibleText(planName);

        WebElement paymentOptionRadio = driver.findElement(By.xpath("//label[contains(text(), '" + paymentOption + "')]/input"));
        paymentOptionRadio.click();
    }

    public void selectClientType(String clientType) {
        WebElement clientTypeRadio = driver.findElement(By.xpath("//label[contains(text(), '" + clientType + "')]/input"));
        clientTypeRadio.click();
    }

    public void clickBuyButton() {
        WebElement buyButton = driver.findElement(By.id("BuyButton"));
        buyButton.click();
    }
}

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class VivacomTest {

    public static void main(String[] args) {
        // Set the path to your ChromeDriver executable.
        System.setProperty("webdriver.chrome.driver", "path_to_chromedriver_executable");

        // Initialize the WebDriver and maximize the browser.
        WebDriver driver = new ChromeDriver();
        driver.manage().window().maximize();

        try {
            // Create an instance of the Page Object.
            VivacomPage vivacomPage = new VivacomPage(driver);

            // Step 1: Load the URL.
            vivacomPage.openHomePage("https://www.vivacom.bg/bg/");

            // Step 2: Navigate to "Devices" > "Mobile phones" from the main menu.
            vivacomPage.navigateToMobilePhones();

            // Step 3: Filter the devices by Brand "Apple."
            vivacomPage.filterByBrand("Apple");

            // Step 4: Filter the devices by color "Blue."
            vivacomPage.filterByColor("Blue");

            // Step 5: Choose device name "APPLE IPHONE 15 PLUS 128GB."
            vivacomPage.chooseDevice("APPLE IPHONE 15 PLUS 128GB");

            // Step 6: Choose mobile plan "Unlimited 300" with "One-time payment."
            vivacomPage.chooseMobilePlan("Unlimited 300", "One-time payment");

            // Step 7: Mark the option "for a client without Vivacom fixed service" and click the "Buy" button.
            vivacomPage.selectClientType("for a client without Vivacom fixed service");
            vivacomPage.clickBuyButton();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Closing browser.
            driver.quit();
        }
    }
}
