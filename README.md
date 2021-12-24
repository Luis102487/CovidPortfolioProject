# CovidPortfolioProject

--Total Cases vs Total Deaths (likelyhood of dying if you contract Covid)
SELECT  location, date, total_cases, total_deaths, round((total_deaths/total_cases)*100, 2) as death_percentage
FROM `luisalva.covid_dataset.covid_deaths` 
order by location, date


-- Total Cases vs Population (Shows percentage of population infected)
SELECT  location, date, total_cases, population, round((total_cases/population)*100, 2) as population_percentage
FROM `luisalva.covid_dataset.covid_deaths` 
order by location, date


-- Countries with Highest Infections Rates Compared to Population
SELECT location, population, max(total_cases) as highestinfectioncount, max(round((total_cases/population)*100, 2)) as cases_percentage
FROM `luisalva.covid_dataset.covid_deaths` 
GROUP BY location, population
order by cases_percentage desc 


-- Countries with Highest Death Counts 
SELECT location, max(total_deaths) as highestdeathcount
FROM `luisalva.covid_dataset.covid_deaths` 
WHERE continent is not NULL  
GROUP BY location
order by highestdeathcount desc 

-- Death Counts by Continent 
SELECT continent, max(total_deaths) as highestdeathcount
FROM `luisalva.covid_dataset.covid_deaths` 
WHERE continent is not NULL  
GROUP BY continent 
order by highestdeathcount desc 

-- Death Counts by Continent (second option)
SELECT location, max(total_deaths) as highestdeathcount
FROM `luisalva.covid_dataset.covid_deaths` 
WHERE continent is NULL  
GROUP BY location 
order by highestdeathcount desc 



-- Countries with Highest Death Percentage per Population
SELECT location, population, max(total_deaths) as highestdeathcount, max(round((total_deaths/population)*100, 2)) as cases_percentage
FROM `luisalva.covid_dataset.covid_deaths` 
GROUP BY location, population
order by cases_percentage desc 
