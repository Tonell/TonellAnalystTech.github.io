Capstone Project: Covid-19 Visual Analysis using Tableau & SQL 

Introduction:
This Capstone project aims to provide a comprehensive visual analysis of Covid-19 data using Tableau and SQL. The data covers the period from the beginning of 2020 to the end of 2021. The dataset includes Covid-19 cases and deaths for various locations globally.

Data Source:
The data used for this analysis is sourced from the 'CovidDeaths' table in the 'PortfolioProject' database. It contains information about new cases, deaths, location, continent, population, and date.

Objective:
The primary objective of this project is to gain insights into the Covid-19 pandemic's impact worldwide. The visualizations will focus on the total number of cases, deaths, and infection percentages, both on a global scale and for specific locations.

Visualization 1: Global Covid-19 Overview

This visualization provides an overview of the total number of Covid-19 cases, total deaths, and the death percentage worldwide.

Visualization 1

SQL Query:

sql
Copy code
Select SUM(new_cases) as total_cases,
       SUM(cast(new_deaths as int)) as total_deaths,
       SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage
From PortfolioProject..CovidDeaths
where continent is not null 
order by 1,2
Visualization 2: Total Deaths by Location

This visualization displays the total number of deaths for each location, excluding 'World,' 'European Union,' and 'International.'

Visualization 2

SQL Query:

sql
Copy code
Select location,
       SUM(cast(new_deaths as int)) as TotalDeathCount
From PortfolioProject..CovidDeaths
Where continent is null 
and location not in ('World', 'European Union', 'International')
Group by location
order by TotalDeathCount desc
Visualization 3: Locations with Highest Infection Rate

This visualization identifies locations with the highest infection rates in terms of the percentage of the population infected.

Visualization 3

SQL Query:

sql
Copy code
Select Location,
       Population,
       MAX(total_cases) as HighestInfectionCount,
       Max((total_cases/population))*100 as PercentPopulationInfected
From PortfolioProject..CovidDeaths
Group by Location, Population
order by PercentPopulationInfected desc
Visualization 4: Evolution of Highest Infection Counts

This visualization tracks the evolution of the highest infection counts for different locations over time.

Visualization 4

SQL Query:

sql
Copy code
Select Location,
       Population,
       date,
       MAX(total_cases) as HighestInfectionCount,
       Max((total_cases/population))*100 as PercentPopulationInfected
From PortfolioProject..CovidDeaths
Group by Location, Population, date
order by PercentPopulationInfected desc
Conclusion:

This Capstone project presented an in-depth visual analysis of Covid-19 data using Tableau and SQL. The visualizations provide valuable insights into the global impact of the pandemic, total deaths by location, and the locations with the highest infection rates. The data visualization helps to understand the severity of the Covid-19 pandemic and its distribution across different regions and countries.
