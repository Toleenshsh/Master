import time
import pandas as pd

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    print('Hello! Let\'s explore some US bikeshare data!')
    
    # Get user input for city (chicago, new york, washington)
    while True:
        city = input('Would you like to see data for Chicago, New York, or Washington? ').lower()
        if city in CITY_DATA:
            break
        else:
            print('Invalid input. Please enter a valid city name.')

    # Get user input for month (all, january, february, ... , june)
    while True:
        month = input('Would you like to filter the data by month? (January, February, March, April, May, June, or "all" for no filter) ').lower()
        if month in ['january', 'february', 'march', 'april', 'may', 'june', 'all']:
            break
        else:
            print('Invalid input. Please enter a valid month name.')

    # Get user input for day of week (all, monday, tuesday, ... sunday)
    while True:
        day = input('Would you like to filter the data by day of the week? (Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, or "all" for no filter) ').lower()
        if day in ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday', 'all']:
            break
        else:
            print('Invalid input. Please enter a valid day of the week.')

    print('-'*40)
    return city, month, day

def load_data(city, month, day):
    # Load data file into a dataframe
    df = pd.read_csv(CITY_DATA[city])

    # Convert the Start Time column to datetime
    df['Start Time'] = pd.to_datetime(df['Start Time'])

    # Extract month, day of the week, and hour from Start Time to create new columns
    df['Month'] = df['Start Time'].dt.month
    df['Day of Week'] = df['Start Time'].dt.weekday_name
    df['Hour'] = df['Start Time'].dt.hour

    # Filter by month if applicable
    if month != 'all':
        # Use the index of the months list to get the corresponding int
        months = ['january', 'february', 'march', 'april', 'may', 'june']
        month = months.index(month) + 1

        # Filter by month to create the new dataframe
        df = df[df['Month'] == month]

    # Filter by day of the week if applicable
    if day != 'all':
        # Filter by day of the week to create the new dataframe
        df = df[df['Day of Week'] == day.title()]

    return df

def time_stats(df):
    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # Display the most common month
    common_month = df['Month'].mode()[0]
    print('Most Common Month:', common_month)

    # Display the most common day of week
    common_day = df['Day of Week'].mode()[0]
    print('Most Common Day of Week:', common_day)

    # Display the most common start hour
    common_hour = df['Hour'].mode()[0]
    print('Most Common Start Hour:', common_hour)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def station_stats(df):
    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # Display the most commonly used start station
    common_start_station = df['Start Station'].mode()[0]
    print('Most Commonly Used Start Station:', common_start_station)

    # Display the most commonly used end station
    common_end_station = df['End Station'].mode()[0]
    print('Most Commonly Used End Station:', common_end_station)

    # Display the most frequent combination of start station and end station trip
    df['Trip'] = df['Start Station'] + ' to ' + df['End Station']
    common_trip = df['Trip'].mode()[0]
    print('Most Frequent Trip:', common_trip)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def trip_duration_stats(df):
    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # Display total travel time
    total_travel_time = df['Trip Duration'].sum()
    print('Total Travel Time:', total_travel_time)

    # Display mean travel time
    mean_travel_time = df['Trip Duration'].mean()
    print('Mean Travel Time:', mean_travel_time)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def user_stats(df):
    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # Display counts of user types
    user_types = df['User Type'].value_counts()
    print('Counts of User Types:\n', user_types)

    # Display counts of gender
    if 'Gender' in df:
        gender_counts = df['Gender'].value_counts()
        print('\nCounts of Gender:\n', gender_counts)

    # Display earliest, most recent, and most common year of birth
    if 'Birth Year' in df:
        earliest_birth_year = df['Birth Year'].min()
        print('\nEarliest Birth Year:', earliest_birth_year)

        most_recent_birth_year = df['Birth Year'].max()
        print('Most Recent Birth Year:', most_recent_birth_year)

        common_birth_year = df['Birth Year'].mode()[0]
        print('Most Common Birth Year:', common_birth_year)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def display_raw_data(df):
    i = 0
    raw_data = input('Would you like to see raw data? Enter yes or no. ').lower()
    while raw_data == 'yes':
        print(df.iloc[i:i+5])
        i += 5
        raw_data = input('Would you like to see more raw data? Enter yes or no. ').lower()

def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        display_raw_data(df)

        restart = input('\nWould you like to restart? Enter yes or no. ').lower()
        if restart != 'yes':
            break

if __name__ == "__main__":
    main()
   
