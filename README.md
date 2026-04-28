# binding-items-using-bindable-layout-in-.net-maui-accordion

**Repository Description**  
This repository contains a .NET MAUI sample that demonstrates how to enable **swipe actions** on dynamically generated accordion items using the Syncfusion **SfAccordion** control.

The sample shows how each `AccordionItem` header can be wrapped inside a `SwipeView`, allowing per‑item swipe actions such as **Favourite**. This approach follows the same conceptual pattern recommended in the official Syncfusion .NET MAUI Accordion documentation.

## Project Overview
The purpose of this project is to help developers understand how to implement swipe‑based interactions on accordion items that are generated from a collection using `BindableLayout.ItemsSource`. This is useful for building modern, interactive user interfaces where item‑level actions should be available without cluttering the content area.

## Features
- Integration of Syncfusion .NET MAUI **SfAccordion**  
- Generate accordion items using `BindableLayout.ItemsSource`  
- Enable swipe gestures using `SwipeView`  
- Bind swipe actions to page‑level commands  
- Pass the current item as a `CommandParameter`  

## Prerequisites
Ensure the following requirements are met before running this project:
- Visual Studio 2022  
- .NET SDK compatible with .NET MAUI  

## Installation and Running the Project
1. Clone or download this repository to your local machine.
2. Open the solution file in Visual Studio 2022.
3. Restore NuGet packages by rebuilding the solution.
4. Build and run the project on a supported .NET MAUI platform.

## About Sample
This project (the `AccordionBindableLayout` sample) demonstrates how to populate `SfAccordion` dynamically by setting `BindableLayout.ItemsSource` to a collection exposed by the page's BindingContext. Each accordion item template binds to a model (for example, an `Employee` or `EmployeeInfo`), and the template provides a header and a content section that both read properties from each model instance.

### Key points covered:
- Using `BindableLayout.ItemsSource` with `SfAccordion` to generate items from a collection
- Defining the `BindableLayout.ItemTemplate` with `DataTemplate` that creates `AccordionItem` elements
- Binding nested controls inside `AccordionItem.Header` and `AccordionItem.Content` to the current item
- Allowing each item to control its expanded state via a bound `IsExpanded` property on the item model

### XAML
Below is the main XAML used in this sample. It demonstrates binding the `SfAccordion` to `Employees` on the page view-model and the `DataTemplate` that produces each `AccordionItem`.

```
    <ContentPage.BindingContext>
        <local:EmployeeDetails/>
    </ContentPage.BindingContext>

    <ContentPage.Content>
        <syncfusion:SfAccordion  x:Name="accordion" BindableLayout.ItemsSource="{Binding Employees}" >
            <BindableLayout.ItemTemplate>
                <DataTemplate>
                    <syncfusion:AccordionItem IsExpanded="{Binding IsExpanded}">
                        <syncfusion:AccordionItem.Header>
                            <Grid  HeightRequest="48">
                                <Label Text="{Binding Name}" Margin="16,14,0,14" CharacterSpacing="0.25" FontFamily="Roboto-Regular"  FontSize="14" />
                            </Grid>
                        </syncfusion:AccordionItem.Header>
                        <syncfusion:AccordionItem.Content>
                            <Grid ColumnSpacing="10" RowSpacing="2" BackgroundColor="#f4f4f4"  >
                                <Grid Margin="16,6,0,0">
                                    <Grid.Resources>
                                        <Style TargetType="Label">
                                            <Setter Property="FontFamily" Value="Roboto-Regular"/>
                                        </Style>
                                    </Grid.Resources>
                                    <Grid.RowDefinitions >
                                        <RowDefinition Height="25"/>
                                        <RowDefinition Height="25"/>
                                        <RowDefinition Height="25"/>
                                        <RowDefinition Height="25"/>
                                        <RowDefinition Height="{OnPlatform Default=90,Android=90,WinUI=70, iOS=100,MacCatalyst=70 }"/>
                                        <RowDefinition Height="Auto"/>
                                    </Grid.RowDefinitions>
                                    <Grid.ColumnDefinitions>
                                        <ColumnDefinition Width="100"/>
                                        <ColumnDefinition Width="100"/>
                                        <ColumnDefinition Width="*"/>
                                    </Grid.ColumnDefinitions>
                                    <Frame  Grid.RowSpan="4" BorderColor="Transparent" Grid.Row="0" Grid.Column="0"  Padding="0" Margin="0,0,0,7">
                                        <Image  Source="{Binding Image}"/>
                                    </Frame>
                                    <Label Text="Position" Grid.Column="1" Grid.Row="0" Margin="6,0,0,0"/>
                                    <Label Text="{Binding Position}" Grid.Row="0" Grid.Column="2"/>
                                    <Label Text="Organization " Grid.Row="1" Grid.Column="1" Margin="6,0,0,0"/>
                                    <Label Text="{Binding OrganizationUnit}" Grid.Row="1" Grid.Column="2"/>
                                    <Label Text="Date Of Birth " Grid.Row="2" Grid.Column="1" Margin="6,0,0,0"/>
                                    <Label Text="{Binding DateOfBirth}" Grid.Row="2" Grid.Column="2"/>
                                    <Label Text="Location " Grid.Row="3" Grid.Column="1" Margin="6,0,0,0"/>
                                    <Label Text="{Binding Location}" Grid.Row="3" Grid.Column="2"/>

                                    <Label Padding="0,10,0,10" Grid.Row="4" Grid.ColumnSpan="3"  LineBreakMode="WordWrap"  
                                            FontSize="14" CharacterSpacing="0.25" VerticalTextAlignment="Center" 
                                                Text="{Binding Description}">
                                    </Label>

                                    <StackLayout Grid.Row="5" Orientation="Horizontal" Margin="0,0,0,12">
                                        <Label Text="&#xe700;" FontSize="16" Margin="0,2,2,2"
                                                   FontFamily='{OnPlatform Android=AccordionFontIcons.ttf#,WinUI=AccordionFontIcons.ttf#AccordionFontIcons,MacCatalyst=AccordionFontIcons,iOS=AccordionFontIcons}'
                                                   VerticalOptions="Center" VerticalTextAlignment="Center"/>
                                        <Label Text="{Binding Phone}" Grid.Column="1" VerticalOptions="Center" CharacterSpacing="0.25" FontSize="14"/>
                                    </StackLayout>
                                </Grid>
                            </Grid>
                        </syncfusion:AccordionItem.Content>
                    </syncfusion:AccordionItem>
                </DataTemplate>
            </BindableLayout.ItemTemplate>
        </syncfusion:SfAccordion>
    </ContentPage.Content>
```

### How it works

- SfAccordion: renders a collection of expandable items. In this example `BindableLayout.ItemsSource` instructs the control to create one `AccordionItem` per element in the `Employees` collection.
- DataTemplate: each item instantiation is defined by the `DataTemplate` inside `BindableLayout.ItemTemplate`. Template bindings (for example `{Binding Name}`, `{Binding Position}`) resolve against the individual model instance.
- IsExpanded control: the sample binds the `IsExpanded` property of each `AccordionItem` to an `IsExpanded` boolean on the model. This allows items to remember or control their expanded state.

## Usage
Run the application to see the SfAccordion populated from the `Info` collection in the ViewModel.  
Swipe left on an accordion header to reveal the **Favourite** action. When triggered, the swipe item executes a command defined on the page’s BindingContext and receives the current item as the command parameter.

This pattern is suitable for:
- Swipe‑to‑favourite or swipe‑to‑action scenarios  
- Contextual item actions  
- Gesture‑driven mobile‑first UIs  

## Documentation
- General Syncfusion documentation:
https://help.syncfusion.com/
- .NET MAUI Introduction:
https://help.syncfusion.com/maui/introduction/overview
- .NET MAUI Accordion Getting Started:
https://help.syncfusion.com/maui/accordion/getting-started

## Additional Resources
- Syncfusion MAUI Accordion feature overview:
https://www.syncfusion.com/maui-controls/maui-accordion

## Troubleshooting
- Ensure the SwipeView is placed inside the AccordionItem.Header.
- Verify that FavouriteCommand exists on the page’s BindingContext.
- Rebuild the solution if swipe gestures are not detected.
- Check output logs for binding or gesture‑related issues.

## Conclusion
I hope you enjoyed learning about how to bind the items source and item template using BindableLayout in .NET MAUI Accordion(SfAccordion).

You can refer to our [.NET MAUI Accordion](https://www.syncfusion.com/maui-controls/maui-accordion) feature tour page to know about its other groundbreaking feature representations. You can also explore our [.NET MAUI Accordion documentation](https://help.syncfusion.com/maui/accordion/getting-started) to understand how to present and manipulate data.

For current customers, you can check out our components from the [License and Downloads](https://www.syncfusion.com/account/login) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our [support forums](https://www.syncfusion.com/forums/), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!