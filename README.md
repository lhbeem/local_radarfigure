# local_radarfigure

Steps for setting up radarfigure on local mac.

1. Clone the deva code base (recursively)
	* probably the master branch will be the correct choice for you. 
	* lhb_hotkey has some additional functionality that suits my needs for picking. It also supports the extended channel needs for multipol.
	* multipol branch as mulitpol functionality, but not all the additional shortcuts I've added for my own personal ease of use. 


	cd {path to install location}
	git clone --recursive https://github.com/UTIG/deva.git deva
	git checkout {branch_name}



2. You'll want to check your python for package dependancies. I'm not sure how you maintain your environment, but you may need to add some of these (not totally sure the version numbers are up to date here) Probably the newest stabile version of the package is appropriate.

matplotlib>=3.0.3
PyQt5>=5.12
numpy>==1.19.4
pyproj>=3.0.0.post1
scipy>=1.5.4
osgeo



3. Then there are some paths within the radarfigure code that need to managed. Probably the easiest thing to do is add symlinks at the paths the radarfigure looks for, instead of changing the radarfigure code itself. 

	mkdir -p $WAIS/targ/xtra/{xped}/CMP
	cd $WAIS/targ/xtra/{xped}/CMP
	ln -s {path to your folder with pik1 data} pik1

	mkdir -p $WAIS/targ/xtra/{xped}/FOC
	cd $WAIS/targ/xtra/{xped}/FOC
	ln -s {path to your folder with foc1 data} Best_Versions



3. editing your .bashrc

	you'll need to add a WAIS shortcut.

	export WAIS=“{path to your ‘WAIS'}"

	probably good to add a shortcut for so you don’t need to type out ‘radarfigure’ every time

		alias rf=“{path to radarFigure.py}"



4. update syst_linux_py to include desired xpeds


	in the folder $WAIS/syst/linux/src/deva/syst_linux_py

	edit waisutils/season.get_season to include desired expedition name(s)

	in radutils/params.py
		add current xped to is_coherent list
		add current xped to get_radar_rates

5. You may need to get the pk3 binary for the hierarchy (/disk/kea/WAIS/syst/linux/bin/pk3) and put it in your $WAIS/syst/linux/bin. This will prevent some ‘pk3 not found’ crashes.
