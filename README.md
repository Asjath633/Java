import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class SimpleCalculator extends Application {

    private TextField display;
    private double firstValue = 0;
    private String operation = "";

    @Override
    public void start(Stage primaryStage) {
        // Create the display
        display = new TextField("0");
        display.setEditable(false);
        display.setStyle("-fx-font-size: 20px;");

        // Create buttons
        Button btn7 = new Button("7");
        Button btn8 = new Button("8");
        Button btn9 = new Button("9");
        Button btnDiv = new Button("/");

        Button btn4 = new Button("4");
        Button btn5 = new Button("5");
        Button btn6 = new Button("6");
        Button btnMul = new Button("*");

        Button btn1 = new Button("1");
        Button btn2 = new Button("2");
        Button btn3 = new Button("3");
        Button btnSub = new Button("-");

        Button btn0 = new Button("0");
        Button btnClear = new Button("Clear");
        Button btnEqual = new Button("=");
        Button btnAdd = new Button("+");

        // Set button actions
        setButtonActions(btn7, btn8, btn9, btn4, btn5, btn6, btn1, btn2, btn3, btn0, btnAdd, btnSub, btnMul, btnDiv, btnEqual, btnClear);

        // Create GridPane layout
        GridPane grid = new GridPane();
        grid.setHgap(5);
        grid.setVgap(5);
        grid.setPadding(new javafx.geometry.Insets(10));

        // Add elements to GridPane
        grid.add(display, 0, 0, 4, 1);
        grid.add(btn7, 0, 1);
        grid.add(btn8, 1, 1);
        grid.add(btn9, 2, 1);
        grid.add(btnDiv, 3, 1);
        grid.add(btn4, 0, 2);
        grid.add(btn5, 1, 2);
        grid.add(btn6, 2, 2);
        grid.add(btnMul, 3, 2);
        grid.add(btn1, 0, 3);
        grid.add(btn2, 1, 3);
        grid.add(btn3, 2, 3);
        grid.add(btnSub, 3, 3);
        grid.add(btn0, 0, 4);
        grid.add(btnClear, 1, 4);
        grid.add(btnEqual, 2, 4);
        grid.add(btnAdd, 3, 4);

        // Set up the scene
        Scene scene = new Scene(grid, 300, 250);
        primaryStage.setTitle("Simple Calc");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void setButtonActions(Button... buttons) {
        for (Button btn : buttons) {
            btn.setOnAction(e -> {
                Button clickedButton = (Button) e.getSource();
                String buttonText = clickedButton.getText();

                switch (buttonText) {
                    case "Clear":
                        display.setText("0");
                        firstValue = 0;
                        operation = "";
                        break;
                    case "=":
                        double secondValue = Double.parseDouble(display.getText());
                        switch (operation) {
                            case "+":
                                display.setText(String.valueOf(firstValue + secondValue));
                                break;
                            case "-":
                                display.setText(String.valueOf(firstValue - secondValue));
                                break;
                            case "*":
                                display.setText(String.valueOf(firstValue * secondValue));
                                break;
                            case "/":
                                if (secondValue != 0) {
                                    display.setText(String.valueOf(firstValue / secondValue));
                                } else {
                                    display.setText("Error");
                                }
                                break;
                        }
                        operation = "";
                        break;
                    case "+", "-", "*", "/":
                        firstValue = Double.parseDouble(display.getText());
                        operation = buttonText;
                        display.setText("0");
                        break;
                    default:
                        if (display.getText().equals("0")) {
                            display.setText(buttonText);
                        } else {
                            display.setText(display.getText() + buttonText);
                        }
                        break;
                }
            });
        }
    }

    public static void main(String[] args) {
        launch(args);
    }
}
