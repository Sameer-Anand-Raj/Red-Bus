# Red-Bus

package Practice;


import java.time.Duration;
import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class Test_Registration {

	public static void main(String[] args) throws InterruptedException {

		//System.setProperty("webdriver.chrome.driver", "src//test//resources//BrowserFile//chromedriver.exe");
		WebDriver driver = new ChromeDriver();

		driver.get("https://www.redbus.in/");
		 driver.manage().window().maximize();
		WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
		Thread.sleep(1000);
		String url = driver.getCurrentUrl();
		System.out.println("Current URL : " + url);
		String title = driver.getTitle();
		System.out.println("Current Title : " + title);

		WebElement logo = driver.findElement(By.cssSelector(".rb_logo"));
		boolean logoDisplay = logo.isDisplayed();
		System.out.println("Logo is Visible : " + logoDisplay);
		Thread.sleep(2000);

		Actions act = new Actions(driver);

		WebElement from = driver.findElement(By.xpath("//input[@id='src']"));
		act.moveToElement(from).click().sendKeys("Patna").build().perform();
		Thread.sleep(3000);

		WebElement selectFirstValueFrom = driver.findElement(By.xpath("//ul[@class='sc-dnqmqq dZhbJF']/li[1]"));
		Thread.sleep(2000);

		act.moveToElement(selectFirstValueFrom).click().build().perform();
		Thread.sleep(3000);

		WebElement to = driver.findElement(By.xpath("//input[@id='dest']"));
		to.click();
		to.sendKeys("Ranchi");
		Thread.sleep(2000);

		WebElement selectFirstValueTo = driver.findElement(By.xpath("//ul[@class='sc-dnqmqq dZhbJF']/li[1]"));
		act.moveToElement(selectFirstValueTo).click().build().perform();
		Thread.sleep(3000);

		WebElement calendarDate = driver.findElement(By.xpath("//div[@id='onwardCal']"));
		calendarDate.click();
		Thread.sleep(2000);

		// ************Select Month & Year************

		String targetMonth = "Sep 2024";
		String targetDate = "20";

		while (true) {

			WebElement currentMonth = driver
					.findElement(By.xpath("//div[@class='DatePicker__MainBlock-sc-1kf43k8-1 hHKFiR']/div[1]/div[2]"));
			String CurrentMonthText = currentMonth.getText();
			System.out.println("Current Month Name :" + CurrentMonthText);
			Thread.sleep(2000);

			if (CurrentMonthText.contains(targetMonth)) {
				System.out.println("Display Targte month & Holidays : " + CurrentMonthText);
				break;
			} else {
				WebElement nextButton = driver
						.findElement(By.xpath("//div[@class='DayNavigator__CalendarHeader-qj8jdz-1 fxvMrr']/div[3]"));
				// act.moveToElement(nextButton).click().build().perform();
				nextButton.click();
				Thread.sleep(2000);
			}
		}

		// ************Select Date from calendar************

		List<WebElement> days = driver.findElements(
				By.xpath("//div[@class='DatePicker__MainBlock-sc-1kf43k8-1 hHKFiR']/div[3]/div/span/div"));
		int dayCount = days.size();
		System.out.println("Total day-List count : " + dayCount);
		Thread.sleep(2000);

		for (int j = 0; j < dayCount; j++) {
			String dayDisplay = days.get(j).getText();
			if (dayDisplay.contains(targetDate)) {
				System.out.println("Display Day : " + dayDisplay);
				// days.get(j).click();
				act.moveToElement(days.get(j)).click().build().perform();
				Thread.sleep(2000);
				break;
			}
		}

		WebElement selectedDateVerify = driver.findElement(By.xpath("//div[@class='sc-kAzzGY cCrHkP']"));
		String dateSelected = selectedDateVerify.getText();
		System.out.println("Selected date is : " + dateSelected);
		Thread.sleep(2000);

		// Search

		WebElement searchButton = driver.findElement(By.xpath("//button[@id='search_button']"));
		searchButton.click();
		Thread.sleep(5000);

		// ***********Total Bus count & Information************

		List<WebElement> totalBusCount = driver
				.findElements(By.xpath("//div[@class='sort-results fl w-80']/div[2]/div/ul/div"));
		// wait.until(ExpectedConditions.visibilityOfAllElements(totalBusCount));
		int totalNumberOfBus = totalBusCount.size();
		System.out.println("Total Number of Bus Available :" + totalNumberOfBus);
		Thread.sleep(2000);

		int k = 1;
		for (int i = 0; i <= totalNumberOfBus; i++) {

				List<WebElement> totalBusInfo = driver.findElements(By.xpath(
						"//div[@class='sort-results fl w-80']/div[2]/div/ul/div[" + k + "]/li/div/div/div[1]/div"));

				int totalInfo = totalBusInfo.size();
				for (int j = 0; j < totalInfo; j++) {

					String info = totalBusInfo.get(j).getText();
					System.out.println("Information " + j + " : " + info);

					Thread.sleep(2000);
				}
				k++;
		}
		 

		// *****************Information of first bus Only********************

		WebElement firstTileOfBus = driver
				.findElement(By.xpath("//div[@class='sort-results fl w-80']/div[2]/div/ul/div[1]"));
		act.moveToElement(firstTileOfBus).perform();
		//String NameOfFirstBus = firstTileOfBus.getText();

		List<WebElement> amenitiesAndOtherInfo = driver.findElements(
				By.xpath("//div[@class='sort-results fl w-80']/div[2]/div/ul/div[1]/li/div/div[2]/div[2]/ul/li"));
		int totalLengthOfInfoTab = amenitiesAndOtherInfo.size();
		for (int p = 0; p < totalLengthOfInfoTab; p++) {

			amenitiesAndOtherInfo.get(p).click();
			Thread.sleep(2000);
			String InfoName = amenitiesAndOtherInfo.get(p).getText();
			System.out.println("INFO Name : " + InfoName);

		}
		
		// *********Click on View seat on First Bus***********
		
		WebElement viewSeat = driver.findElement(By.xpath("//div[@class='sort-results fl w-80']/div[2]/div/ul/div[1]/li/div/div[2]/div[1]"));
    	viewSeat.click();

		// driver.quit();
	}

}



