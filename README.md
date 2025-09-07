# data-template-selector-treeview-xamarin
This repository demonstrates how to apply a DataTemplateSelector in the Xamarin.Forms SfTreeView control. It provides a sample implementation that dynamically selects and applies different data templates to tree nodes based on their type or properties, enabling flexible and context-aware UI customization for hierarchical data.

## Sample

### XAML
```xaml
<ContentPage.Resources>
        <ResourceDictionary>
            <local:ItemTemplateSelector x:Key="ItemTemplateSelector" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <ContentPage.Content>
        <Grid>
            <syncfusion:SfTreeView x:Name="TreeView" ItemHeight="40"
                                   AutoExpandMode="RootNodesExpanded"
                                   ChildPropertyName="SubFiles"
                                   ItemTemplateContextType="Node"
                                   ItemsSource="{Binding ImageNodeInfo}" Indentation="20" 
                                 ExpanderWidth="40" ItemTemplate="{StaticResource ItemTemplateSelector}">
            </syncfusion:SfTreeView>
        </Grid>
    </ContentPage.Content>
```

### ItemTemplateSelector
```csharp
public class ItemTemplateSelector : DataTemplateSelector
{
    public DataTemplate Template1 { get; set; }
    public DataTemplate Template2 { get; set; }
    public ItemTemplateSelector()
    {
        this.Template1 = new DataTemplate(typeof(Template1));
        this.Template2 = new DataTemplate(typeof(Template2));
    }
    protected override DataTemplate OnSelectTemplate(object item, BindableObject container)
    {
        var treeviewNode = item as TreeViewNode;
        if (treeviewNode == null)
            return null;
        if (treeviewNode.Level == 0)
            return Template1;
        else
            return Template2;
    }
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for Xamarin](https://help.syncfusion.com/xamarin/system-requirements)

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
