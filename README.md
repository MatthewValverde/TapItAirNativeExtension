
#TapIt AIR Native Extension Plugin
##Introduction
This is an Air Native Extension (ane) for TapIt.
Please see instructions on how to install the ane below.

##Basic Installation
Add the TapItAir.ane to your Flash Builder project under project - properties - build path - Native Extensions -
In your project <project_name>-app.xml and within the tags: 

	<android><manifestAdditions><manifest>
add:
	<application>
		<activity android:name="com.tapit.adview.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation"/>
	</application>

##Implementation
Simple example:

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
 

* auto escape: if enabled (default) this will escape all variables in the template output.
* auto reload: if enabled (default) this will only regenerate the cached template if the source file has changed.
* cache: the location where to place the cached templates.
* charset: the charset you wish to use, default is the current directory.
* debug: if enabled this will make some extra variables available.
