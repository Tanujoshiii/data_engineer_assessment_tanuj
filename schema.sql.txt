CREATE DATABASE IF NOT EXISTS propertydb;
USE propertydb;

CREATE TABLE properties (
    property_id BIGINT PRIMARY KEY,
    listing_id VARCHAR(255),
    title VARCHAR(255),
    description TEXT,
    property_type VARCHAR(100),
    status VARCHAR(100),
    created_at DATETIME,
    updated_at DATETIME
);

CREATE TABLE addresses (
    address_id BIGINT AUTO_INCREMENT PRIMARY KEY,
    property_id BIGINT,
    street VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    zipcode VARCHAR(50),
    country VARCHAR(100),
    latitude DECIMAL(10,6),
    longitude DECIMAL(10,6),
    FOREIGN KEY(property_id) REFERENCES properties(property_id)
);

CREATE TABLE valuations (
    valuation_id BIGINT AUTO_INCREMENT PRIMARY KEY,
    property_id BIGINT,
    estimated_value DECIMAL(15,2),
    valuation_date DATE,
    FOREIGN KEY(property_id) REFERENCES properties(property_id)
);

CREATE TABLE hoa (
    hoa_id BIGINT AUTO_INCREMENT PRIMARY KEY,
    property_id BIGINT,
    hoa_exists BOOLEAN,
    monthly_fee DECIMAL(10,2),
    hoa_name VARCHAR(255),
    FOREIGN KEY(property_id) REFERENCES properties(property_id)
);
