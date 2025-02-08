interface INFA is IERC721 {
    /// REQUIRED INTERFACES

    /// @notice Get the agent's current experience level
    /// @param tokenId The identifier for the agent
    /// @return The agent's experience level (0 to 10000)
    function getExperience(uint256 tokenId) external view returns (uint256);

    /// @notice Get the agent's attributes
    /// @param tokenId The identifier for the agent
    /// @return names Array of attribute names
    /// @return weights Array of attribute weights (in basis points)
    /// @return thresholds Array of correlation thresholds
    /// @return dataSources Array of data source identifiers
    function getAttributes(uint256 tokenId) external view returns (
        string[] memory names,
        uint256[] memory weights,
        uint256[] memory thresholds,
        string[] memory dataSources
    );

    /// @notice Evolve the agent based on performance metrics
    /// @param tokenId The identifier for the agent
    /// @param metrics Array of performance metrics (in basis points)
    function evolve(uint256 tokenId, uint256[] calldata metrics) external;

    /// EVENTS

    /// @notice Emitted when an agent evolves
    event Evolution(
        uint256 indexed tokenId,
        uint256 newExperience,
        uint256[] metrics
    );

    /// @notice Emitted when an agent's attributes are updated
    event AttributeUpdate(
        uint256 indexed tokenId,
        string[] names,
        uint256[] newWeights
    );
}
