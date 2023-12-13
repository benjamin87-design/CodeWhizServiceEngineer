---
title: "Scheduler with Supabase"
date: 2023-11-07
tags: [ ".NET", "MAUI", "calendar" ]
summary: "Step by step tutorial of how to create a scheduler by yourself and fill it with appointments"
categories: [".Net Maui Tutorial" ]
draft: false
---

## Introduction

.NET MAUI (Multi-platform App UI) is a modern framework for building crossplatform mobile and desktop applications. It is the evolution of Xamarin.Forms and is designed to create applications that can run on multiple platforms. including iOS, Android, and Windows. With .NET MAUI, developers can write code once and deploy it on different platforms, reducing development time and effort. It provides a rich set of UI controls, native performance, and access to platform-specific APIs, making it an ideal choice for building robust and feature-rich applications.

Syncfusion Scheduler is a powerful UI control that allows developers to display and manage appointments and events in a visually appealing and user-friendly way. It provides various scheduling views such as day, week, workweek, month, and timeline, enabling users to easily navigate and interact with their schedule. The scheduler control supports features like recurring appointments, drag-and-drop functionality, resource grouping, and customizable appearance, making it suitable for a wide range of scenarios, including calendar apps, project management tools, and booking systems.

When used together, .NET MAUI and Syncfusion Scheduler enable developers to create cross-platform applications with interactive and professional-looking scheduling features. By leveraging the MVVM pattern, it ensures a separation of concerns, making the code more mainainable and testable. Additionally, integrating Supabase as a data provider enables seamless synchronization of appointments between the app and the Supabase database.

With the convenience and flexibility of .NET MAUI and the feature-rich Syncfusion Scheduler control,developers can build highly functional and visually appealing scheduling applications that target multiple platforms with ease.

## Step 1: Setup the Project

1. Create a new .NET MAUI project in Visual Studio or your preferred IDE.
2. Install the Syncfusion.SfScheduler.Maui package from NuGet to add the Syncfusion Scheduler control to your project.
3. Make sure to install all required packages and dependencies for Syncfusion Scheduler.
4. Install the Supabase.NET package from NuGet(`SupabaseClient` and `SupabaseClient.Extensions`) to connect with the Supabase database.

## Step 2: Configure MVVM Pattern

1. Create a new folder in your project called "Models" to store your data models.
2. Create a new folder called "ViewModels" to store your view models.
3. Inside the "ViewModels" folder, create a new class called "SchedulerViewModel".

```csharp
using Supabase;
using Supabase.Models;
using System.Collections.ObjectModel;

namespace YourApp.ViewModels
{
    public class SchedulerViewModel: ViewModelBase
    {
        private ObservableCollection<Appointment>Appointments
        {
            get{return _appointments;}
            set{_appointments = value; OnPropertyChanged();}
        }

        private SupabaseClient supabaseClient;

        public SchedulerViewModel()
        {
            //Initialize your Supabase client with your project URL and API key
            supabaseClient = new SupabaseClient("YOUR_PROJECT_URL", "YOUR_API_KEY);
            Appointments = new ObservableCollection<Appointment>();

            //Fetch appointments from Supabase
            FetchAppointments();
        }

        private async void FetchAppointments()
        {
            var response = await _supabaseClient
    .From<WorkingTime>()
    .Select("*")
    .Get();

//if response is successful load each to list
if (response.ResponseMessage.IsSuccessStatusCode)
{
    foreach (var item in response.Models)
    {
        //customer is subject, starttime is starttime plus date and endtime is endtime plus date 
        WorkingTimes.Add(new Appointment);
    }
}
```

## Step 3: Create the Scheduler View

1. Open MainPage.xaml in the shared project.
2. Inside the `<ContentPage` tags, add the namespace for Syncfusion Scheduler.
```csharp
xmlns:sfScheduler="clr-namespace:Syncfusion.Maui.Schedule;assembly=Syncfusion.SfScheduler.Maui"
```
3. Add the Scheduler control to your view:
```csharp
<sfScheduler:SfScheduler x:Name="scheduler">
```

## Step 4: Bind Scheduler to ViewModel

1. In MainPage.xaml.cs, set the BindingContext of the scheduler to the SchedulerViewModel:
```csharp
using YourApp.ViewModels

namespace YourApp.Views
{
    public partial class MainPage: ContentPage
    {
        public MainPage(SchedulerViewModel viewModel)
        {
            InitializeComponent();
            BindingContext = viewModel
        }
    }
}
```
2. In MainPage.xaml add
```csharp

    xmlns:vm="clr-namespace:YourApp.ViewModels"
    x:DataType="vm:SchedulerViewModel"
```

## Step 5: Define the Data Model

1. In the "Models" folder, create a new class called "Appointment" to represent a single appointment.
2. Define properties in the "Appointment" class such as "Subject", "Location", "StartTime", "EndTime", etc.

```csharp
namespace YourApp.Models
{
    public class Appointment
    {
        public string Subject {get;set;}
        public string Location {get;set;}
        public DateTime StartTime {get;set;}
        public DateTime EndTime {get;set;}
    }
}
```

## Step 6: Implement Data Binding

1. In MainPage.xaml, bind the Appointments collection from the ViewModel to the scheduler control using the ItemSource property:
```csharp
ItemsSource="{Binding Appointments}"
```
2. Define the mapping of appointment properties to the corresponding properties in the Scheduler control.
```csharp
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:sfScheduler="clr-namespace:Syncfusion.Maui.Schedule;assembly=Syncfusion.SfScheduler.Maui"
             x:Class="YourApp.Pages.MainPage">
    <ContentPage.Content>
        <sfScheduler:SfScheduler
            x:Name="Scheduler"
            AppointmentsSource="{Binding Appointments}"
            View="Week">
        <sfScheduler:SfScheduler.AppointmentMapping>
            <sfScheduler:SchedulerAppointmentMapping
                Background="Background"
                EndTime="To"
                EndTimeZone="EndTimeZone"
                Id="Id"
                IsAllDay="IsAllDay"
                RecurrenceExceptionDates="RecurrenceExceptions"
                RecurrenceId="RecurrenceId"
                RecurrenceRule="RecurrenceRule"
                StartTime="From"
                StartTimeZone="StartTimeZone"
                Subject="EventName"
                TextColorMapping="TextColor" />
            </sfScheduler:SfScheduler.AppointmentMapping>
        </sfScheduler:SfScheduler>
    </ContentPage.Content>
</ContentPage>
```
## Step 7: Use Supabase as Data Provider

1. Initialize the Supabase client in SchedulerViewModel.cs using your Supabase project URL and API key.
2. Use the Supabase client to fetch the appointment data from Supabase and populate the Appointments collection.
3. Implement methods in SchedulerViewModel.cs to create, update, and delete appointments in the Supabase database.
```csharp
using Supabase;
using Supabase.Models;
using System.Collections.ObjectModel;
namespace YourApp.ViewModels
{
    public class SchedulerViewModel : ViewModelBase
    {
        private ObservableCollection<Appointment> _appointments;
        public ObservableCollection<Appointment> Appointments
        {
            get { return _appointments; }
            set { _appointments = value; OnPropertyChanged(); }
        }
        private SupabaseClient supabaseClient;
        public SchedulerViewModel()
        {
            supabaseClient = new SupabaseClient("YOUR_PROJECT_URL", "YOUR_API_KEY");
            Appointments = new ObservableCollection<Appointment>();
            FetchAppointments(); // Fetch appointments from Supabase
        }
        private async Task FetchAppointments()
        {
            var response = await supabaseClient
                .From("appointments")
                .Select("*")
                .Get();
            if (response.IsSuccess)
            {
                Appointments.Clear();
                foreach (var appointment in response.Data)
                {
                    Appointments.Add(appointment.ToObject<Appointment>());
                }
            }
        }
        public async Task<bool> CreateAppointment(Appointment appointment)
        {
            var response = await supabaseClient
                .From("appointments")
                .Insert(new List<Appointment> { appointment })
                .Execute();
            
            return response.IsSuccess;
        }
        public async Task<bool> UpdateAppointment(Appointment appointment)
        {
            var response = await supabaseClient
                .From("appointments")
                .Update(appointment)
                .Execute();
            return response.IsSuccess;
        }
        public async Task<bool> DeleteAppointment(Appointment appointment)
        {
            var response = await supabaseClient
                .From("appointments")
                .Delete(appointment)
                .Execute();
            return response.IsSuccess;
        }
    }
}
```

## Step 8: Display the Scheduler

1. Build and run your application to see the Syncfusion Scheduler with your appointments displayed.
2. Test CRUD operations to create, update, and delete appointments using the Syncfusion Scheduler control and Supabase as the data provider.

## Congratulations! 

You have successfully integrated Syncfusion Scheduler with the MVVM pattern and used Supabase as the data provider in your .NET MAUI application. Adapt the Supabase integration as needed for your specific use case.