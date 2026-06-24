from django.db import models

# Patient Model
class Patient(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
    gender = models.CharField(max_length=10)
    contact = models.CharField(max_length=15)

    def __str__(self):
        return self.name


# Blood Test Model
class BloodTest(models.Model):
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    test_name = models.CharField(max_length=100)
    test_date = models.DateField()
    status = models.CharField(max_length=20, default="Pending")

    def __str__(self):
        return self.test_name


# Result Model
class Result(models.Model):
    blood_test = models.OneToOneField(BloodTest, on_delete=models.CASCADE)
    hemoglobin = models.FloatField()
    wbc_count = models.IntegerField()
    rbc_count = models.FloatField()
    platelet_count = models.IntegerField()
    remarks = models.TextField()

    def __str__(self):
        return f"Result - {self.blood_test.test_name}"
