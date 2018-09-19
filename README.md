
```
import com.google.gwt.core.client.EntryPoint;
import com.google.gwt.user.client.ui.Label;
import com.google.gwt.user.client.ui.RootPanel;

public class LabelNoLineReturnExample implements EntryPoint {

  @Override
  public void onModuleLoad() {
    String s = "The cow jumped over the moon. The school had many kids in it. Someone was eating lunch in the field.";
    
    Label label = new Label(s);
    // ~~~ Turn off word wrapping
    label.setWordWrap(false);
    
    RootPanel.get().add(label);
  }
  
}
```
