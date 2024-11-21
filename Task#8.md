CREATE SCHEMA tour_agency;

CREATE TABLE tour_agency.clients(
  "client_id" bigserial PRIMARY KEY, 
  "first_name" varchar(50),
  "last_name" varchar(50),
  "phone" varchar(15)
);

CREATE TABLE tour_agency.agents (
  agent_id BIGSERIAL  PRIMARY KEY,
  first_name varchar(50),
  last_name varchar(50),
  phone varchar(15),
  commiton_rate float
);

CREATE TABLE tour_agency.resorts (
  resort_id BIGSERIAL PRIMARY KEY,
  resort_name varchar(150) UNIQUE NOT NULL,
  quality integer NOT NULL,
  type varchar(50) NOT NULL,
  country varchar(50) NOT NULL,
  region varchar(30),
  city varchar(50),
  street varchar(100),
  house_number varchar(3)
);

CREATE TABLE tour_agency.offers (
  offer_id BIGSERIAL  PRIMARY KEY,
  resort_id bigint,
  offer_name varchar(255) NOT NULL,
  offer_price decimal(10, 2) NOT NULL,
  FOREIGN KEY (resort_id) REFERENCES tour_agency.resorts(resort_id),
  UNIQUE (resort_id, offer_name)
);

CREATE TABLE tour_agency.photos(
  "photo_id" bigserial PRIMARY KEY, 
  "photo_title" varchar(50),
  "photo_file" varchar,
  "resort_id" bigint,
  FOREIGN KEY (resort_id) REFERENCES tour_agency.resorts(resort_id)
);

CREATE TABLE tour_agency.comments(
  "comment_id" bigserial PRIMARY KEY, 
  "comment_text" text,
  "photo_id" bigint,
  "client_id" bigint,
  FOREIGN KEY (photo_id) REFERENCES tour_agency.photos(photo_id),
  FOREIGN KEY (client_id) REFERENCES tour_agency.clients(client_id)
);

CREATE TABLE tour_agency.tags(
  "tag_id" bigserial PRIMARY KEY, 
  "tag_name" varchar(50),
  "photo_id" bigint,
  FOREIGN KEY (photo_id) REFERENCES tour_agency.photos(photo_id)
);

CREATE TABLE tour_agency.contracts (
    contract_id bigserial PRIMARY KEY,
    agent_id integer,
    client_id integer,
    offer_id integer,
    signing_date date,
    rest_period integer,
    FOREIGN KEY (agent_id) REFERENCES tour_agency.agents(agent_id),
    FOREIGN KEY (client_id) REFERENCES tour_agency.clients(client_id),
    FOREIGN KEY (offer_id) REFERENCES tour_agency.offers(offer_id)
);
