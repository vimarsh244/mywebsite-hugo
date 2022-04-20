+++
author = "Vimarsh"
categories = []
date = ""
description = ""
images = []
tags = []
title = "WordPress CapRover Configuration for ARM CPUs"
url = "/notes/wordpres-caprover-config"

+++
For Wordpress (with Database)  
using MariaDB for Databse

    captainVersion: 4
    services:
        $$cap_appname-db:
            image: arm64v8/mariadb:$$cap_database_version
            volumes:
                - $$cap_appname-db-data:/var/lib/mysql
            restart: always
            environment:
                MYSQL_ROOT_PASSWORD: $$cap_db_pass
                MYSQL_DATABASE: wordpress
                MYSQL_USER: $$cap_db_user
                MYSQL_PASSWORD: $$cap_db_pass
            caproverExtra:
                notExposeAsWebApp: 'true'
        $$cap_appname-wordpress:
            depends_on:
                - $$cap_appname-db
            image: arm64v8/wordpress:$$cap_wp_version
            volumes:
                - $$cap_appname-wp-data:/var/www/html
            restart: always
            environment:
                WORDPRESS_DB_HOST: srv-captain--$$cap_appname-db:3306
                WORDPRESS_DB_USER: $$cap_db_user
                WORDPRESS_DB_PASSWORD: $$cap_db_pass
    caproverOneClickApp:
        variables:
            - id: $$cap_db_user
              label: Database user
              defaultValue: wordpressuser
              validRegex: /^([a-zA-Z0-9])+$/
            - id: $$cap_db_pass
              label: Database password
              description: ''
              validRegex: /^(\w|[^\s"'\\])+$/
            - id: $$cap_wp_version
              label: WordPress Version
              defaultValue: '5.8'
              description: Check out their Docker page for the valid tags https://hub.docker.com/r/arm64v8/wordpress/tags
              validRegex: /^([^\s^\/])+$/
            
            - id: $$cap_database_version
              label: Database Version, for MariaDB
              defaultValue: 'latest'
              description: We are USING MARIADB| Check out the Docker pages for the valid tags https://hub.docker.com/r/arm64v8/mariadb/tags
              validRegex: /^([^\s^\/])+$/
        instructions:
            start: >-
                WordPress is an online, open source website creation tool written in PHP. But in non-geek speak, it’s probably the easiest and most powerful blogging and website content management system (or CMS) in existence today.
                Enter your WordPress Configuration parameters and click on next. A MariaDB (database) and a WordPress container will be created for you. The process will take about a minute for the process to finish.
            end: >
                Wordpress is deployed and available as $$cap_appname-wordpress . 
                IMPORTANT: It will take up to 2 minutes for WordPress to be ready. Before that, you might see a 502 error page.
        displayName: WordPress
    
        description: WordPress is one of the most popular a content management system (CMS) based on PHP.
        documentation: Taken from https://docs.docker.com/compose/wordpress/. Port mapping removed from WP as it is no longer needed
    
    