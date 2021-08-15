# README.md-lenjerii-test
package Test;

import org.junit.Assert;
import org.junit.Test;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import java.util.List;
import java.util.Random;

public class LenjeriiCalitateTest {
    public WebDriver driver;

    @Test
    public void InregistrationTest() {
        //descarcam driverul
        //setam driverul de chrome

        System.setProperty("webdriver.chrome.driver", "C:\\Automation\\chromedriver\\chromedriver.exe");
        driver = new ChromeDriver();
        driver.get("https://lenjerii-calitate.ro/lenjerii-de-pat/");

        //maximize driver
        driver.manage().window().maximize();

        //declaram elementele de pe pagina

        WebElement ChatCloseButton = driver.findElement(By.xpath("//div[@class='et_cookie_law_button_wrapper ty-center']/a"));
        ChatCloseButton.click();

        String ExpectedPageTitle = "Lenjerii de pat";
        String ActualPageTitle = driver.getTitle();
        Assert.assertEquals("Page whas not dislayed", ExpectedPageTitle, ActualPageTitle);

        WebElement SearchField = driver.findElement(By.xpath("//input[@id='search_input']"));
        SearchField.click();
        SearchField.sendKeys("lenjerii pat");

        WebElement SearchButton = driver.findElement(By.xpath("//button[@title='Cautati']/i"));
        SearchButton.click();

        WebElement OferteButton = driver.findElement(By.xpath("//a[contains(text(), 'Oferte')]"));
        OferteButton.click();

        List<WebElement> CategoriiList = driver.findElements(By.xpath("//div[@class='clearfix']//li/a/span"));
        CategoriiList.get(1).click();

        List<WebElement> ListaProduse = driver.findElements(By.xpath("//div[@class='preview-image']/div"));
        Random Product = new Random();
        int IndexProduseRandom = Product.nextInt(ListaProduse.size());
        ListaProduse.get(IndexProduseRandom).click();

        WebElement AddtoCartButton = driver.findElement(By.xpath("//a[@class='ty-btn et-icon-atc cm-submit text-button vs-text-w-icon ']"));
        new WebDriverWait(driver, 10).until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//a[@class='ty-btn et-icon-atc cm-submit text-button vs-text-w-icon ']")));
        AddtoCartButton.click();

        WebDriverWait wait = new WebDriverWait(driver,3);
        WebElement CloseButton = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//span[@class='cm-notification-close close']")));
        CloseButton.click();

        WebElement PaginaDeStartButton = driver.findElement(By.xpath("//a[contains(text(),'Pagina de start')]"));
        new WebDriverWait(driver,20).until(ExpectedConditions.elementToBeClickable(PaginaDeStartButton));
        PaginaDeStartButton.click();
        driver.navigate().to("https://lenjerii-calitate.ro/");

        WebElement BanerButton = driver.findElement(By.xpath("//div[@id='banner_original_172']"));
        ((JavascriptExecutor)driver).executeScript("arguments[0].scrollIntoView(true)",BanerButton);
        BanerButton.click();

        WebElement CartButton = driver.findElement(By.xpath("//a[@id='sw_dropdown_150']"));
        CartButton.click();

        List<WebElement> VeziCosButton = driver.findElements(By.xpath("//a[contains(text(),'Vizualizati cosul')]"));
        VeziCosButton.get(0).click();
        driver.navigate().to("https://lenjerii-calitate.ro/cart/");

        WebElement GolitiCosulButton = driver.findElement(By.xpath("//a[contains(text(),'Goliti cosul')]"));
        GolitiCosulButton.click();

        driver.switchTo().alert().getText();
        driver.switchTo().alert().accept();

        String ExpectedProdusStersMessage = "Cosul dvs.este gol";
        new WebDriverWait(driver,10).until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//p[contains(text(),'Cosul dvs.este gol')]")));
        WebElement ProdusStersMessage = driver.findElement(By.xpath("//p[contains(text(),'Cosul dvs.este gol')]"));
        String ActualProdusStersMessage = ProdusStersMessage.getText();
        Assert.assertEquals("Message was not corect display", ExpectedProdusStersMessage, ActualProdusStersMessage);

        driver.close();


    }
}

}
