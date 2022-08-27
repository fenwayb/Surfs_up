<h1 Align="Center">
  
  Surfs Up

  # Overview
  
  <p>For this project we were tasked with using SQLAlchemy and an SQLite database to query weather data and then present it using Flask</p>
  
  ## Results
<p>The code successfully pulls data from the database which is then converted into a Pandas dataframe for ease of viewing</p>


  ### Tempature
<p> To begin with we compared tempatures in Hawaii from June and December over the span of 5 years. There is suprisingly less variation than I thought between the peak of summer and the peak of winter but it makes sense given Hawaii's location. </p>

| June  | Dec |
| ------------- | ------------- |
| ![Describe June Temps](https://user-images.githubusercontent.com/106105597/187043938-c6dfa3a3-c7ec-4193-8063-3913dfc32589.png)  | ![Describe Dec Temps](https://user-images.githubusercontent.com/106105597/187043940-a0d0ccbf-1027-475f-837b-ff890b3da44d.png)  |

### Percipitation
 <p> We also compared percipitation levels from the same place at the same time and over the same span. It is clear that December has a higher percipitation level on average than June.</p>

| June  | Dec |
| ------------- | ------------- |
| ![Describe June Prcp](https://user-images.githubusercontent.com/106105597/187044231-138e9528-365e-4366-9fea-04469f6b1142.png)  | ![Describe Dec Prcp](https://user-images.githubusercontent.com/106105597/187044228-73878ce9-711f-43a1-a271-fd2f8474af95.png)|



### By Year Code
<p> I made a function to break the queries up into each individual year to see year on year change for any of these values. The code is as follows</p>

```
def value_by_yearsf(query):
    years = []
    value_by_year = []
    df = pd.DataFrame(query, columns=["date","value"])
    df.set_index(df['date'], inplace=True)
    df = df.sort_index()
    for year in query:
        just_year = year[0]
        just_year = re.split('\-', just_year)
        if just_year[0] not in years:
            years.append(just_year[0])
    for year in years:
        value_df = df.filter(like=year, axis=0)
        value = value_df.mean(numeric_only=True)
        value_by_year.append({f'{value.values[0]}'})
    
    return years, value_by_year
```
### Temp By Year
<p> The year by year change was not as noticable as I would have thought. I imagine the small timeframe makes it hard to see any real trend. Notice that the December data only goes to 2016</p>

| June  | Dec |
| ------------- | ------------- |
| ![Mean June Temp By Year](https://user-images.githubusercontent.com/106105597/187044285-f54e97f9-9817-4761-9a5d-38a9c76bb60d.png) |![Mean Dec Temp by Year](https://user-images.githubusercontent.com/106105597/187044367-ad8835e7-bfc5-4b43-b1d9-f64716553376.png)|

### Percipitation by Year
<p> Like tempature, I think the timeframe was too small to see any real significant trend. Again, notice that the December data only goes to 2016</p>

| June  | Dec |
| ------------- | ------------- |
| ![Mean June Prcp by Year](https://user-images.githubusercontent.com/106105597/187044311-61474007-0e7e-4fd5-9e0f-76d6bee99247.png) | ![Mean Dec Prcp by Year](https://user-images.githubusercontent.com/106105597/187044315-aac91056-699c-42d1-bd33-b4ecff776379.png)|
