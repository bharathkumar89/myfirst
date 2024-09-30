# myfirst
first project in frontend

import java.util.Scanner;

// Base class for Insurance
class Insurance {
    private String insuranceNo;
    private String insuranceName;
    private Double amountCovered;

    public String getInsuranceNo() {
        return insuranceNo;
    }

    public void setInsuranceNo(String insuranceNo) {
        this.insuranceNo = insuranceNo;
    }

    public String getInsuranceName() {
        return insuranceName;
    }

    public void setInsuranceName(String insuranceName) {
        this.insuranceName = insuranceName;
    }

    public Double getAmountCovered() {
        return amountCovered;
    }

    public void setAmountCovered(Double amountCovered) {
        this.amountCovered = amountCovered;
    }
}

// Class for Motor Insurance
class MotorInsurance extends Insurance {
    private Double idv;  // Insured Declared Value
    private Float depPercent;

    public Double getIdv() {
        return idv;
    }

    public void setIdv(Double idv) {
        this.idv = idv;
    }

    public Float getDepPercent() {
        return depPercent;
    }

    public void setDepPercent(Float depPercent) {
        this.depPercent = depPercent;
    }

    public double calculatePremium() {
        idv = getAmountCovered() - ((getAmountCovered() * depPercent) / 100);
        return 0.03 * idv;  // 3% of IDV
    }
}

// Class for Life Insurance
class LifeInsurance extends Insurance {
    private int policyTerm;
    private Float benefitPercent;

    public int getPolicyTerm() {
        return policyTerm;
    }

    public void setPolicyTerm(int policyTerm) {
        this.policyTerm = policyTerm;
    }

    public Float getBenefitPercent() {
        return benefitPercent;
    }

    public void setBenefitPercent(Float benefitPercent) {
        this.benefitPercent = benefitPercent;
    }

    public double calculatePremium() {
        return (getAmountCovered() - ((getAmountCovered() * benefitPercent) / 100)) / policyTerm;
    }
}

// Main class
public class Program {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Get general insurance details
        System.out.print("Insurance Number: ");
        String insuranceNo = scanner.nextLine();
        System.out.print("Insurance Name: ");
        String insuranceName = scanner.nextLine();
        System.out.print("Amount Covered: ");
        Double amountCovered = scanner.nextDouble();

        System.out.println("Select");
        System.out.println("1. Life Insurance");
        System.out.println("2. Motor Insurance");
        int option = scanner.nextInt();

        // Create appropriate insurance object based on user selection
        if (option == 1) {  // Life Insurance
            LifeInsurance lifeInsurance = new LifeInsurance();
            lifeInsurance.setInsuranceNo(insuranceNo);
            lifeInsurance.setInsuranceName(insuranceName);
            lifeInsurance.setAmountCovered(amountCovered);
            
            System.out.print("Policy Term: ");
            lifeInsurance.setPolicyTerm(scanner.nextInt());
            System.out.print("Benefit Percent: ");
            lifeInsurance.setBenefitPercent(scanner.nextFloat());

            double calculatedPremium = addPolicy(lifeInsurance);
            System.out.println("Calculated Premium: " + calculatedPremium);

        } else if (option == 2) {  // Motor Insurance
            MotorInsurance motorInsurance = new MotorInsurance();
            motorInsurance.setInsuranceNo(insuranceNo);
            motorInsurance.setInsuranceName(insuranceName);
            motorInsurance.setAmountCovered(amountCovered);
            
            System.out.print("Depreciation Percent: ");
            motorInsurance.setDepPercent(scanner.nextFloat());

            double calculatedPremium = addPolicy(motorInsurance);
            System.out.println("Calculated Premium: " + calculatedPremium);
        } else {
            System.out.println("Invalid option selected.");
        }

        scanner.close();
    }

    public static double addPolicy(Insurance ins) {
        if (ins instanceof LifeInsurance) {
            return ((LifeInsurance) ins).calculatePremium();
        } else if (ins instanceof MotorInsurance) {
            return ((MotorInsurance) ins).calculatePremium();
        }
        return 0;
    }
}

