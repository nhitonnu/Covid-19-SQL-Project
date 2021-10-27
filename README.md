# Covid-19-SQL-Project
/*Queries used for Tableau Project*/

--1. Show Total Cases, Total Deaths, Death Percentage 

Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage

From PortfolioProject..CovidDeaths

where continent is not null 

order by 1,2

--2. Show Location, Total Death Count

Select location, SUM(cast(new_deaths as int)) as TotalDeathCount

From PortfolioProject..CovidDeaths

Where continent is null 

and location not in ('World', 'European Union', 'International')

Group by location

order by TotalDeathCount desc

--3. Show Location, Population, Highest Infection Count, Percentage of Population Infected

Select Location, Population, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected

From PortfolioProject..CovidDeaths

Group by Location, Population

order by PercentPopulationInfected desc

--4. Show Location, Population, Date, Highest Infection Count, Percentage of Population Infected

Select Location, Population,date, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected

From PortfolioProject..CovidDeaths

Group by Location, Population, date

order by PercentPopulationInfected desc

