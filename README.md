# binding-items-using-bindable-layout-in-.net-maui-accordion

This sample demonstrates how to bind an items source and item template to the Syncfusion SfAccordion control in a .NET MAUI application using BindableLayout.

It shows a practical pattern: the accordion is driven by a ViewModel collection and each generated `AccordionItem` uses data bindings for both the header and the content. The example is adapted from Syncfusion's Accordion guidance and follows the same conceptual approach as the Xamarin.Forms sample — see the official UG for more details:

- [Getting Started with MAUI Accordion](https://help.syncfusion.com/maui/accordion/getting-started)

## Overview

This project (the `AccordionBindableLayout` sample) demonstrates how to populate `SfAccordion` dynamically by setting `BindableLayout.ItemsSource` to a collection exposed by the page's BindingContext. Each accordion item template binds to a model (for example, an `Employee` or `EmployeeInfo`), and the template provides a header and a content section that both read properties from each model instance.

Key points covered:

- Using `BindableLayout.ItemsSource` with `SfAccordion` to generate items from a collection
- Defining the `BindableLayout.ItemTemplate` with `DataTemplate` that creates `AccordionItem` elements
- Binding nested controls inside `AccordionItem.Header` and `AccordionItem.Content` to the current item
- Allowing each item to control its expanded state via a bound `IsExpanded` property on the item model

## XAML

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

## How it works

- SfAccordion: renders a collection of expandable items. In this example `BindableLayout.ItemsSource` instructs the control to create one `AccordionItem` per element in the `Employees` collection.
- DataTemplate: each item instantiation is defined by the `DataTemplate` inside `BindableLayout.ItemTemplate`. Template bindings (for example `{Binding Name}`, `{Binding Position}`) resolve against the individual model instance.
- IsExpanded control: the sample binds the `IsExpanded` property of each `AccordionItem` to an `IsExpanded` boolean on the model. This allows items to remember or control their expanded state.

##### Conclusion
I hope you enjoyed learning about how to bind the items source and item template using BindableLayout in .NET MAUI Accordion(SfAccordion).

You can refer to our [.NET MAUI Accordion](https://www.syncfusion.com/maui-controls/maui-accordion) feature tour page to know about its other groundbreaking feature representations. You can also explore our [.NET MAUI Accordion documentation](https://help.syncfusion.com/maui/accordion/getting-started) to understand how to present and manipulate data.

For current customers, you can check out our components from the [License and Downloads](https://www.syncfusion.com/account/login) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our [support forums](https://www.syncfusion.com/forums/), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!

