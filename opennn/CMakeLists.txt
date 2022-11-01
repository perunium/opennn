cmake_minimum_required(VERSION 3.14)

project(opennn)

find_package(Eigen3 REQUIRED)

add_library(opennn
adaptive_moment_estimation.cpp
bounding_layer.cpp
codification.cpp
conjugate_gradient.cpp
convolutional_layer.cpp
correlations.cpp
cross_entropy_error.cpp
data_set.cpp
flatten_layer.cpp
genetic_algorithm.cpp
gradient_descent.cpp
growing_inputs.cpp
growing_neurons.cpp
inputs_selection.cpp
layer.cpp
learning_rate_algorithm.cpp
levenberg_marquardt_algorithm.cpp
long_short_term_memory_layer.cpp
loss_index.cpp
mean_squared_error.cpp
minkowski_error.cpp
model_selection.cpp
neural_network.cpp
neurons_selection.cpp
normalized_squared_error.cpp
numerical_differentiation.cpp
opennn_strings.cpp
optimization_algorithm.cpp
perceptron_layer.cpp
pooling_layer.cpp
probabilistic_layer.cpp
pruning_inputs.cpp
quasi_newton_method.cpp
recurrent_layer.cpp
region_based_object_detector.cpp
response_optimization.cpp
scaling.cpp
scaling_layer.cpp
statistics.cpp
stochastic_gradient_descent.cpp
sum_squared_error.cpp
tensor_utilities.cpp
testing_analysis.cpp
text_analytics.cpp
tinyxml2.cpp
training_strategy.cpp
unit_testing.cpp
unscaling_layer.cpp
weighted_squared_error.cpp
)

set_target_properties(opennn PROPERTIES PUBLIC_HEADER "config.h;half.hpp;adaptive_moment_estimation.h;bounding_layer.h;codification.h;conjugate_gradient.h;convolutional_layer.h;correlations.h;cross_entropy_error.h;data_set.h;flatten_layer.h;genetic_algorithm.h;gradient_descent.h;growing_inputs.h;growing_neurons.h;inputs_selection.h;layer.h;learning_rate_algorithm.h;levenberg_marquardt_algorithm.h;long_short_term_memory_layer.h;loss_index.h;mean_squared_error.h;minkowski_error.h;model_selection.h;neural_network.h;neurons_selection.h;normalized_squared_error.h;numerical_differentiation.h;opennn_strings.h;optimization_algorithm.h;perceptron_layer.h;pooling_layer.h;probabilistic_layer.h;pruning_inputs.h;quasi_newton_method.h;recurrent_layer.h;region_based_object_detector.h;response_optimization.h;scaling.h;scaling_layer.h;statistics.h;stochastic_gradient_descent.h;sum_squared_error.h;tensor_utilities.h;testing_analysis.h;text_analytics.h;tinyxml2.h;training_strategy.h;unit_testing.h;unscaling_layer.h;weighted_squared_error.h"
)

target_include_directories(opennn
                           PUBLIC
                           "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
                           "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
)

add_library(opennn::opennn ALIAS opennn)
install(
    TARGETS opennn
    EXPORT opennn-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/opennn"
)

set(CMAKE_EXPORT_PACKAGE_REGISTRY ON)

configure_file("${CMAKE_CURRENT_LIST_DIR}/opennn-config.cmake.in" "${CMAKE_BINARY_DIR}/opennn-config.cmake" @ONLY)
install(FILES "${CMAKE_BINARY_DIR}/opennn-config.cmake" DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/opennn")

install(EXPORT opennn-targets
    FILE opennn-targets.cmake
    NAMESPACE opennn::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/opennn
)
