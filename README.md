project title:Emergency Ambulance tracker

core function:"this java application manages a fleet of ambulances by tracking theur locations and dispatching them to emergency calls.
              it uses centalised ambulance tracker to store vehicle data and provides a console based interfaces for users to view available
              units or request immidiate assistance"

key files: AMBULANCE TRACKER.JAVA

technical details:
        language:java
        object oriented programming(OOP)
        classes and objects are used


import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Ambulance {
    private String id;
    private String location;
    
    public Ambulance(String id, String location) {
        this.id = id;
        this.location = location;
    }

    public String getId() {
        return id;
    }

    public String getLocation() {
        return location;
    }

    public void updateLocation(String newLocation) {
        this.location = newLocation;
    }
}

class EmergencyCall {
    private String callerName;
    private String location;
    
    public EmergencyCall(String callerName, String location) {
        this.callerName = callerName;
        this.location = location;
    }

    public String getCallerName() {
        return callerName;
    }

    public String getLocation() {
        return location;
    }
}

class AmbulanceTracker {
    private List<Ambulance> ambulances;

    public AmbulanceTracker() {
        ambulances = new ArrayList<>();
    }

    public void addAmbulance(Ambulance ambulance) {
        ambulances.add(ambulance);
    }

    public Ambulance findNearestAmbulance(String emergencyLocation) {
        // For simplicity, we just return the first ambulance
        // In a real-world scenario, you would implement distance calculations
        return ambulances.isEmpty() ? null : ambulances.get(0);
    }

    public void displayAmbulances() {
        System.out.println("Available ambulances:");
        for (Ambulance ambulance : ambulances) {
            System.out.println("Ambulance ID: " + ambulance.getId() + ", Location: " + ambulance.getLocation());
        }
    }
}

public class EmergencyAmbulanceTrackerApp {
    public static void main(String[] args) {
        AmbulanceTracker tracker = new AmbulanceTracker();
        tracker.addAmbulance(new Ambulance("A001", "Downtown"));
        tracker.addAmbulance(new Ambulance("A002", "Uptown"));
        tracker.addAmbulance(new Ambulance("A003", "Suburbs"));

        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        while (running) {
            System.out.println("Emergency Ambulance Tracker");
            System.out.println("1. View Available Ambulances");
            System.out.println("2. Call for Emergency Ambulance");
            System.out.println("3. Exit");
            System.out.print("Select an option: ");
            
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    tracker.displayAmbulances();
                    break;
                case 2:
                    System.out.print("Enter your name: ");
                    String callerName = scanner.nextLine();
                    System.out.print("Enter your location: ");
                    String location = scanner.nextLine();
                    
                    EmergencyCall call = new EmergencyCall(callerName, location);
                    Ambulance nearestAmbulance = tracker.findNearestAmbulance(location);
                    
                    if (nearestAmbulance != null) {
                        System.out.println("Sending " + nearestAmbulance.getId() + " to " + location);
                    } else {
                        System.out.println("No ambulances available at the moment.");
                    }
                    break;
                case 3:
                    running = false;
                    System.out.println("Exiting the application.");
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
        
        scanner.close();
 }
}
        
