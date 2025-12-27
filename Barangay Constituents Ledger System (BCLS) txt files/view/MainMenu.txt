package view;

import javax.swing.*;
import javax.swing.border.EmptyBorder;
import java.awt.*;

public class MainMenu extends JFrame {

    private RegistrationForm regWindow;
    private RecordsWindow recordsWindow;
    private PurokCensusWindow censusWindow;
    private CategoryReportWindow reportWindow;

    public MainMenu() {
        setTitle("Barangay Constituents Ledger System (BCLS)");
        setSize(850, 700); 
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new BorderLayout());

        JPanel headerPanel = new JPanel();
        headerPanel.setLayout(new BoxLayout(headerPanel, BoxLayout.Y_AXIS));
        headerPanel.setBorder(new EmptyBorder(30, 0, 30, 0)); 
        
        headerPanel.setBackground(new Color(44, 62, 80)); 

        JLabel lblLogo = new JLabel();
        try {
            java.net.URL imgUrl = getClass().getResource("/res/logo.png");
            
            if (imgUrl != null) {
                ImageIcon originalIcon = new ImageIcon(imgUrl);
                Image scaledImg = originalIcon.getImage().getScaledInstance(130, 130, Image.SCALE_SMOOTH);
                lblLogo.setIcon(new ImageIcon(scaledImg));
            } else {
                System.err.println("Error: Could not find image at /res/logo.png");
            }
        } catch (Exception e) {
             e.printStackTrace();
        }
        lblLogo.setAlignmentX(Component.CENTER_ALIGNMENT);
    
        JLabel lblTitle = new JLabel("Barangay Constituents Ledger System (BCLS)");
        lblTitle.setFont(new Font("Arial", Font.BOLD, 32));
        lblTitle.setAlignmentX(Component.CENTER_ALIGNMENT);

        lblTitle.setForeground(Color.WHITE); 

        JLabel lblTagline = new JLabel("Empowering barangay service through precise data.");
        lblTagline.setFont(new Font("Arial", Font.ITALIC, 16));
        lblTagline.setAlignmentX(Component.CENTER_ALIGNMENT);
      
        lblTagline.setForeground(Color.WHITE);

        headerPanel.add(lblLogo);
        headerPanel.add(Box.createRigidArea(new Dimension(0, 20))); 
        headerPanel.add(lblTitle);
        headerPanel.add(Box.createRigidArea(new Dimension(0, 10))); 
        headerPanel.add(lblTagline);
        add(headerPanel, BorderLayout.NORTH);

        JPanel mainButtonContainer = new JPanel(new GridBagLayout());
        mainButtonContainer.setBorder(new EmptyBorder(20, 50, 50, 50)); 
        
        mainButtonContainer.setBackground(new Color(236, 240, 241));

        JPanel gridPanel = new JPanel(new GridLayout(2, 2, 20, 20)); 

        gridPanel.setOpaque(false); 
        
        JButton btnRegister = createStyledButton("Register Constituent");
        JButton btnRecords = createStyledButton("Master Ledger");
        JButton btnCensus = createStyledButton("Census by Purok");
        JButton btnReports = createStyledButton("Category Reports");

        gridPanel.add(btnRegister);
        gridPanel.add(btnRecords);
        gridPanel.add(btnCensus);
        gridPanel.add(btnReports);

        GridBagConstraints gbc = new GridBagConstraints();
        gbc.gridx = 0; 
        gbc.gridy = 0;
        
        mainButtonContainer.add(gridPanel, gbc);

        JButton btnExit = createStyledButton("Exit System");
        btnExit.setPreferredSize(new Dimension(0, 60)); 
        
        gbc.gridy = 1; 
        gbc.insets = new Insets(20, 0, 0, 0); 
        gbc.fill = GridBagConstraints.HORIZONTAL; 
        mainButtonContainer.add(btnExit, gbc);

        add(mainButtonContainer, BorderLayout.CENTER);

        btnRegister.addActionListener(e -> {
            if (regWindow == null || !regWindow.isVisible()) {
                regWindow = new RegistrationForm(); 
                regWindow.setVisible(true);
            } else {
                regWindow.toFront(); 
                regWindow.requestFocus();
            }
        });
        btnRecords.addActionListener(e -> {
            if (recordsWindow == null || !recordsWindow.isVisible()) {
                recordsWindow = new RecordsWindow();
                recordsWindow.setVisible(true);
            } else {
                recordsWindow.toFront();
                recordsWindow.requestFocus();
            }
        });

        btnCensus.addActionListener(e -> {
            if (censusWindow == null || !censusWindow.isVisible()) {
                censusWindow = new PurokCensusWindow();
                censusWindow.setVisible(true);
            } else {
                censusWindow.toFront();
                censusWindow.requestFocus();
            }
        });

        btnReports.addActionListener(e -> {
            if (reportWindow == null || !reportWindow.isVisible()) {
                reportWindow = new CategoryReportWindow();
                reportWindow.setVisible(true);
            } else {
                reportWindow.toFront();
                reportWindow.requestFocus();
            }
        });

        btnExit.addActionListener(e -> {
            int confirm = JOptionPane.showConfirmDialog(this,
                "Are you sure you want to exit the system?",
                "Confirm Exit", JOptionPane.YES_NO_OPTION);
            if (confirm == JOptionPane.YES_OPTION) {
                System.exit(0);
            }
        });

        setVisible(true);
    }

    private JButton createStyledButton(String text) {
        JButton btn = new JButton(text);
        btn.setFont(new Font("Arial", Font.PLAIN, 18)); 
        btn.setFocusPainted(false);

        btn.setPreferredSize(new Dimension(250, 80)); 
        return btn;
    }
}