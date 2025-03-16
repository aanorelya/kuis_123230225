import javax.swing.*;
import java.awt.event.*;

public class SeleksiMagangg extends JFrame {
    private JTextField nameField, nimField, writingField, codingField, interviewField;
    private JComboBox<String> divisionBox;
    private JButton submitButton;

    public SeleksiMagangg() {
        setTitle("Seleksi Magang IT");
        setSize(400, 350);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);

        JLabel nameLabel = new JLabel("Nama:");
        nameLabel.setBounds(20, 20, 100, 20);
        add(nameLabel);

        nameField = new JTextField();
        nameField.setBounds(150, 20, 200, 20);
        add(nameField);

        JLabel nimLabel = new JLabel("NIM:");
        nimLabel.setBounds(20, 50, 100, 20);
        add(nimLabel);

        nimField = new JTextField();
        nimField.setBounds(150, 50, 200, 20);
        add(nimField);

        JLabel divisionLabel = new JLabel("Divisi:");
        divisionLabel.setBounds(20, 80, 100, 20);
        add(divisionLabel);

        divisionBox = new JComboBox<>(new String[]{"Android Developer", "Web Developer"});
        divisionBox.setBounds(150, 80, 200, 20);
        add(divisionBox);

        JLabel writingLabel = new JLabel("Writing Score:");
        writingLabel.setBounds(20, 110, 100, 20);
        add(writingLabel);

        writingField = new JTextField();
        writingField.setBounds(150, 110, 200, 20);
        add(writingField);

        JLabel codingLabel = new JLabel("Coding Score:");
        codingLabel.setBounds(20, 140, 100, 20);
        add(codingLabel);

        codingField = new JTextField();
        codingField.setBounds(150, 140, 200, 20);
        add(codingField);

        JLabel interviewLabel = new JLabel("Interview Score:");
        interviewLabel.setBounds(20, 170, 100, 20);
        add(interviewLabel);

        interviewField = new JTextField();
        interviewField.setBounds(150, 170, 200, 20);
        add(interviewField);

        submitButton = new JButton("Submit");
        submitButton.setBounds(150, 210, 100, 30);
        add(submitButton);

        submitButton.addActionListener(e -> evaluate());

        setVisible(true);
    }

    private void evaluate() {
        String name = nameField.getText().trim();
        String nim = nimField.getText().trim();
        String division = (String) divisionBox.getSelectedItem();

        if (name.isEmpty() || nim.isEmpty() || writingField.getText().trim().isEmpty() ||
                codingField.getText().trim().isEmpty() || interviewField.getText().trim().isEmpty()) {
            JOptionPane.showMessageDialog(this, "Semua kolom harus diisi.");
            return;
        }

        try {
            int writingScore = Integer.parseInt(writingField.getText().trim());
            int codingScore = Integer.parseInt(codingField.getText().trim());
            int interviewScore = Integer.parseInt(interviewField.getText().trim());

            if (writingScore < 0 || writingScore > 100 ||
                codingScore < 0 || codingScore > 100 ||
                interviewScore < 0 || interviewScore > 100) {
                JOptionPane.showMessageDialog(this, "Nilai harus berada di antara 0 hingga 100.");
                return;
            }

            double finalScore;
            if (division.equals("Android Developer")) {
                finalScore = (writingScore * 0.2) + (codingScore * 0.5) + (interviewScore * 0.3);
            } else {  // Web Developer
                finalScore = (writingScore * 0.4) + (codingScore * 0.35) + (interviewScore * 0.25);
            }

            if (finalScore >= 85) {
                JOptionPane.showMessageDialog(this, "DITERIMA! Selamat " + name + " (" + nim + "), Anda diterima sebagai " + division + ".");
            } else {
                JOptionPane.showMessageDialog(this, "TIDAK DITERIMA! Maaf " + name + " (" + nim + "), Anda tidak diterima sebagai " + division + ".");
            }

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Nilai harus berupa angka.");
        }
    }

    public static void main(String[] args) {
        new SeleksiMagangg();
    }
    
}

