
#TapIt AIR Native Extension Plugin
##Introduction
This is an Air Native Extension (ane) for TapIt.
Please see instructions on how to install the ane below.

##Basic Installation

Create an AIR mobile project for Android.

Add the TapItAir.ane to your project build path.

For example: Flash Builder project under project - properties - build path - Native Extensions

The TapItAir native extension requires these permissions and a TapIt Android Activity to run:

* android.permission.INTERNET
* android.permission.ACCESS_NETWORK_STATE
* android.permission.READ_PHONE_STATE
* com.tapit.adview.AdActivity

The permisions and Activity must be located in the android manifest for the AIR application.

The Andorid manifest is loacted in your project <project_name>-app.xml: 

	<android>
		<manifestAdditions>
			<manifest>
	
			</manifest>
		</manifestAdditions>
	</android>
	
within the manifest tags add:

	<uses-permission android:name="android.permission.INTERNET"></uses-permission>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
	<uses-permission android:name="android.permission.READ_PHONE_STATE"></uses-permission>
			
and the activity:
			
	<application>
		<activity android:name="com.tapit.adview.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation"/>
	</application>
	
To finally appear as:

	<android>
        <colorDepth>16bit</colorDepth>
        <manifestAdditions><![CDATA[
			<manifest android:installLocation="auto">
			    
			    <uses-permission android:name="android.permission.INTERNET"></uses-permission>
				<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
				<uses-permission android:name="android.permission.READ_PHONE_STATE"></uses-permission>
			    		
				<application>
				     <activity android:name="com.tapit.adview.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation"/>
				</application>
				
			</manifest>
		]]></manifestAdditions>
    </android>

##ActionScript Implementation

There can only be one instance of any of the availble ad options.

You can add 1 banner, 1 ad alert and 1 full screen add-- at the same time, but you are unable to add multiple instances of any ad option.  
i.e.-- 2+ banners, 2+ ad alerts, or 2+ fullscreen ads.

####Banner example:

	package
	{
		import flash.display.Sprite;
		import com.tapit.air.TapItAir;
	
		public class MyTapItApp extends Sprite
		{
			public function MyTapItApp()
			{		
				TapItAir.addBanner();
			}
		}
	}
	
####Example for Banner sizing, position and zone:

	package
	{
		import flash.display.Sprite;
		import com.tapit.air.TapItAir;
		import com.tapit.air.BannerSizes;
	
		public class MyTapItApp extends Sprite
		{
			public function MyTapItApp()
			{		
				TapItAir.addBanner(BannerSizes.IPHONE_BANNER, "top", "7979"); // size 320 x 50; posistion on top; publisher zone = 7979.
				
				//TapItAir.addBanner(BannerSizes.AUTOSIZE_AD, "bottom", "7979"); // default
			}
		}
	}

####Banner size options:
* BannerSizes.AUTOSIZE_AD = auto
* BannerSizes.IPHONE_BANNER = 320 x 50
* BannerSizes.XL_BANNER = 300x50
* BannerSizes.LARGE_BANNER = 216x36
* BannerSizes.MEDIUM_BANNER = 168x28
* BannerSizes.SMALL_BANNER = 120x20
	
####Ad Alert example:

	package
	{
		import flash.display.Sprite;
		import com.tapit.air.TapItAir;
	
		public class MyTapItApp extends Sprite
		{
			public function MyTapItApp()
			{		
				TapItAir.addAlert();
				
				// To change publisher zone -- TapItAir.addAlert("7984");
			}
		}
	}

####FullScreen Ad example:
	
	package
	{
		import flash.display.Sprite;
		import com.tapit.air.TapItAir;
		import com.tapit.air.BannerSizes;
	
		public class MyTapItApp extends Sprite
		{
			public function MyTapItApp()
			{		
				TapItAir.addFullScreen();
				
				// To change publisher zone -- TapItAir.addFullScreen("7979");
			}
		}
	}
	
####Receiving call back example:

	package
	{
		import flash.display.Sprite;
		import flash.events.StatusEvent;
		import com.tapit.air.TapItAir;
	
		public class MyTapItApp extends Sprite
		{
			public function MyTapItApp()
			{		
				TapItAir.addEventListener(StatusEvent.STATUS, statusUpdate);
			
				TapItAir.addBanner();
			}
		
			private function statusUpdate(event:StatusEvent):void
			{
				if(event.code=="BANNER_ADDED")
				{
					// do something;
				}
				
				if(event.code=="BANNER_CLOSED")
				{
					// do something;
				}
			}
		}
	}
	
####Call back available codes:

* BANNER_ADDED
* BANNER_CLOSED
* BANNER_ERROR
* BANNER_CLICKED
* BANNER_START_FULLSCREEN
* BANNER_ADDED_FULLSCREEN
* BANNER_DISMISS_FULLSCREEN
* ALERT_ADDED
* ALERT_CLOSED
* ALERT_ERROR
* FULLSCREEN_START
* FULLSCREEN_LOADING
* FULLSCREEN_READY
* FULLSCREEN_ADDED
* FULLSCREEN_ERROR
* FULLSCREEN_CLICKED
* FULLSCREEN_DISMISSED
* FULLSCREEN_CLOSED

