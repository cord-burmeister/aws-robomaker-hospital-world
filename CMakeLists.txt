 ################################################################################
# Set minimum required version of cmake, project name and compile options
################################################################################
cmake_minimum_required(VERSION 3.8)
project(aws_robomaker_hospital_world)

################################################################################
# Find ament packages and libraries for ament and system dependencies
################################################################################
find_package(ament_cmake REQUIRED)

#find_package(gazebo_ros REQUIRED)

exec_program("python3 -m pip install -r ${CMAKE_CURRENT_SOURCE_DIR}/requirements.txt")
exec_program("python3 ${CMAKE_CURRENT_SOURCE_DIR}/fuel_utility.py download -m XRayMachine -m IVStand -m BloodPressureMonitor -m BPCart -m BMWCart -m CGMClassic -m StorageRack -m Chair -m InstrumentCart1 -m Scrubs -m PatientWheelChair -m WhiteChipChair -m TrolleyBed -m SurgicalTrolley -m PotatoChipChair -m VisitorKidSit -m FemaleVisitorSit -m AdjTable -m MopCart3 -m MaleVisitorSit -m Drawer -m OfficeChairBlack -m ElderLadyPatient -m ElderMalePatient -m InstrumentCart2 -m MetalCabinet -m BedTable -m BedsideTable -m AnesthesiaMachine -m TrolleyBedPatient -m Shower -m SurgicalTrolleyMed -m StorageRackCovered -m KitchenSink -m Toilet -m VendingMachine -m ParkingTrolleyMin -m PatientFSit -m MaleVisitorOnPhone -m FemaleVisitor -m MalePatientBed -m StorageRackCoverOpen -m ParkingTrolleyMax -d ${CMAKE_CURRENT_SOURCE_DIR}/fuel_models --verbose")

################################################################################
# Install
################################################################################

install(DIRECTORY launch models fuel_models worlds photos
	DESTINATION share/${PROJECT_NAME}
)

ament_export_dependencies(ament_cmake)
#ament_export_dependencies(gazebo_ros)

# Following hooks are used to ensure that the correct environment variables
# will be set by exectuting 'source install/setup.bash' after compilation.
# When using this template for your project, change the filenames of the
# files in the 'hooks' folder, to correspond to your project name.
ament_environment_hooks("${CMAKE_CURRENT_SOURCE_DIR}/hooks/${PROJECT_NAME}.dsv.in")
ament_environment_hooks("${CMAKE_CURRENT_SOURCE_DIR}/hooks/${PROJECT_NAME}.sh.in")
ament_environment_hooks("${CMAKE_CURRENT_SOURCE_DIR}/hooks/${PROJECT_NAME}-fuel.dsv.in")
ament_environment_hooks("${CMAKE_CURRENT_SOURCE_DIR}/hooks/${PROJECT_NAME}-fuel.sh.in")

################################################################################
# Macro for ament package
################################################################################
ament_package()
