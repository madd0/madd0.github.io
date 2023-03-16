---
title: 'Partially Coloured TextBlock'
date: Thu, 03 Mar 2011 14:19:19 +0000
draft: false
tags: ['.NET', 'English', 'Human–computer interaction', 'ProgressBar', 'StackOverflow', 'Technology', 'TextBlock', 'WPF']
---

I stumbled upon [an interesting question on StackOverflow](http://stackoverflow.com/questions/5169829/partial-text-color-update) where someone is using a series of `TextBlock`s in a `StackPanel` to show them side by side and would like part of the displayed text to be coloured with one colour and the rest with another.

There has got to be a thousand ways to do this, but it got me thinking of how _I_ would do it, and especially, how to do it quickly because I have a job besides StackOverflow ![Smile with tongue out](http://blog.madd0.com/images/Windows-Live-Writer/Partially-colored-TextBlock_B304/wlEmoticon-smilewithtongueout_2.png)

Here’s my take on the problem.

First, I get rid of all those TextBlocks and keep only one. This is most likely what the StackOverflow user wanted to do anyways and it will allow me to do stuff such as display text based on a binding. The user also wanted a “bindable” percentage to determine how much of the text is coloured, so I’ll set up a quick UI that will display my text and use a slider to define this percentage.

```
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="auto" />
    <RowDefinition Height="auto" />
    <RowDefinition />
  </Grid.RowDefinitions>

  <TextBlock
    FontSize="34" FontWeight="Bold"
    Text="{Binding Value, ElementName=slider, StringFormat={}{0:p0} of this text is coloured}"></TextBlock>

  <Slider x:Name="slider" Grid.Row="1" Minimum="0" Maximum="1" Value="0.4" />
</Grid>
So now we have a TextBlock with text bound to a certain percentage. All that’s left is colouring the text appropriately.

You could do this pretty easily with just XAML and a few bindings:

```
<TextBlock FontSize="34" FontWeight="Bold"
           Text="{Binding Value, ElementName=slider, StringFormat={}{0:p0} of this text is coloured}">
  <TextBlock.Foreground>
    <LinearGradientBrush EndPoint="1 0">
      <GradientStop Color="BurlyWood" />
      <GradientStop Color="BurlyWood" Offset="{Binding Value, ElementName=slider}" />
      <GradientStop Color="Beige" Offset="{Binding Value, ElementName=slider}" />
      <GradientStop Color="Beige" Offset="1" />
    </LinearGradientBrush>
  </TextBlock.Foreground>
</TextBlock>
```
But, where’s the fun in that? Besides, it’s not very reusable. So, let’s make some changes.

The easiest way to modify an existing control’s behaviour in WPF, without creating a custom control, is using attached properties. So that’s what I’m going to do.

```
public static class PercentageColor
{
    // Using a DependencyProperty as the backing store for Color1.  This enables animation, styling, binding, etc...
    public static readonly DependencyProperty Color1Property =
        DependencyProperty.RegisterAttached("Color1", typeof(Color), typeof(PercentageColor), new UIPropertyMetadata(Colors.Black, OnPropertyChanged));

    // Using a DependencyProperty as the backing store for Color2.  This enables animation, styling, binding, etc...
    public static readonly DependencyProperty Color2Property =
        DependencyProperty.RegisterAttached("Color2", typeof(Color), typeof(PercentageColor), new UIPropertyMetadata(Colors.Red, OnPropertyChanged));

    // Using a DependencyProperty as the backing store for Percentage.  This enables animation, styling, binding, etc...
    public static readonly DependencyProperty PercentageProperty =
        DependencyProperty.RegisterAttached("Percentage", typeof(float), typeof(PercentageColor), new UIPropertyMetadata(0f, OnPropertyChanged));

    public static Color GetColor1(DependencyObject obj)
    {
        return (Color)obj.GetValue(Color1Property);
    }

    public static void SetColor1(DependencyObject obj, Color value)
    {
        obj.SetValue(Color1Property, value);
    }

    public static Color GetColor2(DependencyObject obj)
    {
        return (Color)obj.GetValue(Color2Property);
    }

    public static void SetColor2(DependencyObject obj, Color value)
    {
        obj.SetValue(Color2Property, value);
    }

    public static float GetPercentage(DependencyObject obj)
    {
        return (float)obj.GetValue(PercentageProperty);
    }

    public static void SetPercentage(DependencyObject obj, float value)
    {
        obj.SetValue(PercentageProperty, value);
    }
}
The class above defines 3 attached properties: Color1, Color2 and Percentage that will be used to define how the text should be coloured.

You probably noticed that there is a method missing, OnPropertyChanged, which is called every time any of the 3 attached properties changes. I left it out for clarity, but here it is:

```
private static void OnPropertyChanged(DependencyObject o, DependencyPropertyChangedEventArgs e)
{
    var target = o as TextBlock;

    if (target == null)
    {
        return;
    }

    var color1 = PercentageColor.GetColor1(o);
    var color2 = PercentageColor.GetColor2(o);
    var percentage = PercentageColor.GetPercentage(o);

    var brush = target.Foreground as LinearGradientBrush;

    if (brush == null)
    {
        var gradient = new LinearGradientBrush();
        gradient.EndPoint = new Point(1, 0);
        gradient.GradientStops.Add(new GradientStop(color1, 0));
        gradient.GradientStops.Add(new GradientStop(color1, percentage));
        gradient.GradientStops.Add(new GradientStop(color2, percentage));
        gradient.GradientStops.Add(new GradientStop(color2, 1));

        target.Foreground = gradient;
    }
    else
    {
        brush.GradientStops\[0\].Color = color1;
        brush.GradientStops\[1\].Color = color1;
        brush.GradientStops\[1\].Offset = percentage;
        brush.GradientStops\[2\].Color = color2;
        brush.GradientStops\[2\].Offset = percentage;
        brush.GradientStops\[3\].Color = color2;
    }
}
When the value of an attached property on TextBlock changed—because of a binding, for example— the above method is fired. There are basically two possible cases:

	1.  We haven’t done our magic, so the text colour is not yet a gradient, in which case the appropriate gradient has to be created.
	2.  Magic has been done, so all we have to do is update the gradient to match the current state of the target’s attached properties.

All that’s left now, is to use the newly created properties on a TextBlock:
```
<TextBlock
  my:PercentageColor.Percentage="{Binding Value, ElementName=slider}"
  my:PercentageColor.Color1="BurlyWood"
  my:PercentageColor.Color2="Beige"
  FontSize="34" FontWeight="Bold"
  Text="{Binding Path=(my:PercentageColor.Percentage),
                 StringFormat={}{0:p0} of this text is coloured,
                 RelativeSource={x:Static RelativeSource.Self}}" />
```
Don’t forget to add the appropriate XML namespace declaration (e.g. xmlns:my="clr-namespace:PercentageColorDemo").

The code could probably use a little bit of refactoring and error handling, but I guess it’s not bad for a demo. You can download the sources here:

[PercentageColorDemo.zip](http://blog.madd0.com/images/Windows-Live-Writer/Partially-colored-TextBlock_B304/PercentageColorDemo_1.zip)

What would you have done different?


```
```
```