#Gradle Scripts for Play! Framework Application

This repo contains a ````build.gradle```` file that contains some useful Gradle snippets to be used for building and packaging a Play! Application.

##build.gradle


**Defining Repositories**

````groovy
buildscript{
  repositories{
		mavenLocal()
		mavenCentral()
	}
}

````
**Taking backup of the public folder**

````groovy
task backupResources {
}

task backupJS(type:Copy){
  from ('public/javascripts') {
		include '*.js'
	}
	into 'resources/javascripts'
}

task backupCSS(type:Copy){
	from ('public/stylesheets') {
		include '*.css'
	}
	into 'resources/stylesheets'
}
````

**Script for Zipping the backup file**

````groovy
task zip(type:Zip){
  baseName = projectDir.name
	version = zipVersion

	from("resources/") {
		into 'resources'
	}

	from('app/controllers/'){
		into 'controllers'
	}

	from('app/views/'){
		exclude 'errors'
		into 'views'
	}

	from('conf/'){
		into 'conf'
	}
	
}
````