# Authentication-GUI
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.HashMap;

public class AuthenticationGUI {

    // Mock database of users
    private static HashMap<String, String> userDatabase = new HashMap<>();

    public static void main(String[] args) {
        // Populate mock user database
        userDatabase.put("admin", "admin123");
        userDatabase.put("teacher", "teacher123");
        userDatabase.put("student", "student123");

        // Create the login frame
        JFrame frame = new JFrame("Timetable Management System - Login");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 250);
        frame.setLayout(new GridBagLayout());
        
        // Create UI components
        JLabel titleLabel = new JLabel("Timetable Management System");
        titleLabel.setFont(new Font("Arial", Font.BOLD, 16));
        JLabel usernameLabel = new JLabel("Username:");
        JLabel passwordLabel = new JLabel("Password:");
        
        JTextField usernameField = new JTextField(15);
        JPasswordField passwordField = new JPasswordField(15);
        
        JButton loginButton = new JButton("Login");
        JButton resetButton = new JButton("Reset");
        
        JLabel statusLabel = new JLabel("");
        statusLabel.setForeground(Color.RED);
        
        // Arrange components in the frame
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        
        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.gridwidth = 2;
        frame.add(titleLabel, gbc);

        gbc.gridwidth = 1;
        gbc.gridx = 0;
        gbc.gridy = 1;
        frame.add(usernameLabel, gbc);

        gbc.gridx = 1;
        gbc.gridy = 1;
        frame.add(usernameField, gbc);

        gbc.gridx = 0;
        gbc.gridy = 2;
        frame.add(passwordLabel, gbc);

        gbc.gridx = 1;
        gbc.gridy = 2;
        frame.add(passwordField, gbc);

        gbc.gridx = 0;
        gbc.gridy = 3;
        frame.add(loginButton, gbc);

        gbc.gridx = 1;
        gbc.gridy = 3;
        frame.add(resetButton, gbc);

        gbc.gridx = 0;
        gbc.gridy = 4;
        gbc.gridwidth = 2;
        frame.add(statusLabel, gbc);

        // Add action listeners
        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                
                if (userDatabase.containsKey(username) && userDatabase.get(username).equals(password)) {
                    statusLabel.setForeground(Color.GREEN);
                    statusLabel.setText("Login successful!");
                    JOptionPane.showMessageDialog(frame, "Welcome, " + username + "!");
                } else {
                    statusLabel.setForeground(Color.RED);
                    statusLabel.setText("Invalid username or password.");
                }
            }
        });

        resetButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                usernameField.setText("");
                passwordField.setText("");
                statusLabel.setText("");
            }
        });

        // Display the frame
        frame.setLocationRelativeTo(null); // Center the frame
        frame.setVisible(true);
    }
}
