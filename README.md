# reproduce-maui-bug

This is a repo to reproduce a potential .NET MAUI bug on macOS.

The MaximumWidthRequest property on the FlexLayout should request a maximum width. On Windows, it works the way I'd expect it to. It doesn't seem to work at all on macOS.

MAUI version:

```
% dotnet workload list

Installed Workload Id      Manifest Version      Installation Source
--------------------------------------------------------------------
maui-maccatalyst           7.0.59/7.0.100        SDK 7.0.200        
maui-ios                   7.0.59/7.0.100        SDK 7.0.200        
maui-android               7.0.59/7.0.100        SDK 7.0.200 
```

Here's an example. This XAML code renders 16 buttons with WidthRequest="100" inside a FlexLayout with MaximumWidthRequest="400":

```
     <FlexLayout Wrap="Wrap" MaximumWidthRequest="400">
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
       <Button BackgroundColor="LightBlue" BorderColor="Black" HeightRequest="100" WidthRequest="100" FontSize="60" />
     </FlexLayout>
```

On Windows this renders exactly the way I expect it to:

<img width="421" alt="image" src="https://user-images.githubusercontent.com/7516297/221907409-95da3a68-1f77-4bfa-a5cf-cf314f733c58.png">

When I resize the window so it's smaller than 400 wide, the buttons wrap as expected.

On macOS using Visual Studo 17.6 Preview (17.6 build 402) installed on clean machine, it looks like this:

<img width="797" alt="image" src="https://user-images.githubusercontent.com/7516297/221908635-6762d7e0-38ef-4686-82a6-2e7d328e1e65.png">

The MaximumWidthRequest property seems to be ignored, and the buttons wrap as if it's not there.

Also, it looks like the `BorderColor="Black"` property in the buttons is being ignored.
